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
  name: "chart",
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
            // 坐标轴指示器，坐标轴触发有效
            type: "shadow" // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        xAxis: {
          type: "category",
          data: []
        },
        yAxis: {
          type: "value"
        },
        series: [
          {
            type: "line",
            data: []
          }
        ]
      });
    },
    setChatData(chat, name, xAxisData, seriesData, color, type) {
      chat.setOption({
        tooltip: {
          trigger: "axis"
        },
        color: [color],
        xAxis: {
          data: xAxisData,
          name: "x"
        },
        yAxis: {
          type: "log",
          name: "y"
        },
        series: [
          {
            name: name,
            data: seriesData,
            type: type
          }
        ]
      });
    },
    update() {
      let XData = this.$props.XData;
      let seriesData = this.$props.seriesData;
      let des = this.$props.des;
      let color = this.$props.color;
      let type = this.$props.type;
      this.setChatData(this.chart, des, XData, seriesData, color, type);
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
    },
    color: {
      type: String,
      default: "#19be6b"
    },
    type: {
      type: String,
      default: "line"
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
