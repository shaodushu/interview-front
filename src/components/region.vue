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
  name: "region",
  data() {
    return {
      chart: null
    };
  },
  methods: {
    createChat(chat) {
      chat.setOption({
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "cross",
            label: {
              backgroundColor: "#6a7985"
            }
          }
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: [],
          name: "x"
        },
        yAxis: {
          type: "value",
          name: "y",
          type: "log"
        },
        series: []
      });
    },
    setChatData(chat, name, xAxisData, seriesData) {
      chat.setOption({
        xAxis: {
          data: xAxisData
        },
        series: seriesData
      });
    },
    update() {
      let XData = this.$props.XData;
      let seriesData = this.$props.seriesData;
      let des = this.$props.des;
      this.setChatData(this.chart, des, XData, seriesData);
    }
  },
  props: {
    XData: {
      type: Array,
      default: []
    },
    seriesData: {
      type: Array,
      default: []
    },
    des: {
      type: String
    }
  },
  watch: {
    XData(data) {
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
