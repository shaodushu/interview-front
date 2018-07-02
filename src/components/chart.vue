<style scoped>
.chart {
  width: inherit;
  height: inherit;
}
</style>
<template>
    <div ref="chart" class="chart"></div>
</template>
<script>
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
          data: [],
        },
        yAxis: {
          type: "value",
        },
        series: [
          {
            name: name,
            type: "line",
            data: []
          }
        ]
      });
    },
    setChatData(chat, name, xAxisData, seriesData, color) {
      chat.setOption({
        color: [color],
        xAxis: {
          data: xAxisData
        },
        series: [
          {
            name: name,
            data: seriesData
          }
        ]
      });
    },
    update() {
      let XData = this.$props.XData;
      let seriesData = this.$props.seriesData;
      let des = this.$props.des;
      let color = this.$props.color;
      this.setChatData(this.chart, des, XData, seriesData, color);
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
