<style scoped>
.chart {
  width: inherit;
  height: inherit;
  min-width: 720px;
  min-height: 260px;
  background: #fff;
}
</style>
<template>
    <div ref="chart" class="chart"></div>
</template>
<script>
/**
 * 柱状图，曲线图
 */
import echarts from "echarts";
export default {
  name: "pie",
  data() {
    return {
      chart: null
    };
  },
  methods: {
    createChat(chat) {
      chat.setOption({
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        series: [
          {
            type: "pie",
            data: [],
            roseType: "radius",
            animationType: "scale",
            animationEasing: "elasticOut",
            animationDelay: function(idx) {
              return Math.random() * 200;
            }
          }
        ]
      });
    },
    setChatData(chat, name, seriesData) {
      chat.setOption({
        series: [
          {
            name: name,
            data: seriesData,
          }
        ]
      });
    },
    update() {
      let seriesData = this.$props.seriesData;
      let des = this.$props.des;
      this.setChatData(this.chart, des, seriesData);
    }
  },
  props: {
    seriesData: {
      type: Array,
      default: []
    },
    des: {
      type: String
    },
  },
  watch: {
    seriesData(data) {
      this.update(this.chart);
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.chart = echarts.init(this.$refs.chart);
      this.createChat(this.chart);
      this.update(this.chart);
      window.addEventListener("resize", () => {
        this.chart.resize();
      });
    });
  }
};
</script>
