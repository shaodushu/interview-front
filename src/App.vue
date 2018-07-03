<template>
  <div id="app">
    <Layout>
            <Sider :width="100">
                <Menu active-name="line" theme="dark" width="auto" @on-select="checkMenu">
                    <MenuItem name="line">曲线图</MenuItem>
                    <MenuItem name="bar">柱状图</MenuItem>
                    <MenuItem name="pie">饼图</MenuItem>
                    <MenuItem name="region">面积图</MenuItem>
                </Menu>
            </Sider>
            <Layout>
                <Content class="app_content">
                    <Chart :XData="chartData.XData" :seriesData="chartData.SeriesData" :des="chartData.des" :type="chartData.type" v-if="chartShow.line.display||chartShow.bar.display"/>
                    <Pie :seriesData="pie.SeriesData" :des="pie.des" v-else-if="chartShow.pie.display"></Pie>
                    <Region :XData="region.XData" :seriesData="region.SeriesData" :des="region.des" v-else></Region>
                </Content>
            </Layout>
        </Layout>   
  </div>
</template>

<script>
import { Chart, Pie ,Region} from "@/components";
import { Layout, Sider, Content, Menu, MenuItem } from "iview";
export default {
  name: "App",
  components: {
    Chart,
    Layout,
    Sider,
    Content,
    Menu,
    MenuItem,
    Pie,
    Region
  },
  data() {
    return {
      chartData: {},
      chartShow: {
        line: {
          display: true
        },
        bar: {
          display: false
        },
        pie: {
          display: false
        },
        region: {
          display: false
        }
      },
      curve: {
        XData: ["A", "B", "C", "D"],
        SeriesData: [820, 932, 901, 333],
        des: "曲线图",
        type: "line"
      },
      columnar: {
        XData: ["系列1", "系列2", "系列3"],
        SeriesData: [820, 932, 901],
        des: "柱状图",
        type: "bar"
      },
      pie: {
        SeriesData: [
          { value: 12, name: "a" },
          { value: 21, name: "b" },
          { value: 23, name: "c" },
          { value: 23, name: "d" }
        ],
        des: "饼图",
        type: "pie"
      },
      region: {
        XData: ['a','b','c','d'],
        SeriesData: [
          {
            name: "a",
            type: "line",
            stack: "总量",
            areaStyle: { normal: {} },
            data: [120, 132, 101, 134, 90, 230, 210]
          },
          {
            name: "b",
            type: "line",
            stack: "总量",
            areaStyle: { normal: {} },
            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: "c",
            type: "line",
            stack: "总量",
            areaStyle: { normal: {} },
            data: [150, 232, 201, 154, 190, 330, 410]
          },
          {
            name: "d",
            type: "line",
            stack: "总量",
            areaStyle: { normal: {} },
            data: [320, 332, 301, 334, 390, 330, 320]
          },
        ],
        des: "柱状图",
        type: "category"
      }
    };
  },
  methods: {
    checkMenu(data) {
      this.chartData = {};
      for (let i in this.chartShow) {
        this.chartShow[i].display = false;
      }
      this.chartShow[data].display = true;
      switch (data) {
        case "line":
          Object.assign(this.chartData, this.curve);
          break;
        case "bar":
          Object.assign(this.chartData, this.columnar);
          break;
        // case 'pie':
        //   //Object.assign(this.chartData, this.pie);
        //   break;
        case "region":
          Object.assign(this.chartData, this.region);
          break;
          break;
      }
    }
  },
  created() {
    Object.assign(this.chartData, this.curve);
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;

  border: 1px solid #d7dde4;
  background: #f5f7f9;
  position: relative;
  border-radius: 4px;
  overflow: hidden;
}
.app_content {
  margin: 20px;
  padding: 20px;
  background: #fff;
  /* min-height: 260px; */
  border-radius: 5px;
  box-shadow: 0 4px 16px 0 #ccc;
}
</style>
