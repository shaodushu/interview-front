<template>
  <div id="app">
    <Layout>
            <Sider :width="100">
                <Menu active-name="1" theme="dark" width="auto" @on-select="checkMenu">
                    <MenuItem name="0">曲线图</MenuItem>
                    <MenuItem name="1">柱状图</MenuItem>
                    <MenuItem name="2">饼图</MenuItem>
                    <MenuItem name="3">面积图</MenuItem>
                </Menu>
            </Sider>
            <Layout>
                <Content class="app_content">
                    <Chart :XData="columnar.XData" :seriesData="columnar.SeriesData" des="当前商店销售量" :style="{background: '#fff', minHeight: '260px',minWidth:'720px'}"/>
                </Content>
            </Layout>
        </Layout>   
  </div>
</template>

<script>
import Chart from "./components/chart";
import { Layout, Sider, Content, Menu, MenuItem } from "iview";
export default {
  name: "App",
  components: {
    Chart,
    Layout,
    Sider,
    Content,
    Menu,
    MenuItem
  },
  data() {
    return {
      columnar: {
        XData: ["系列1", "系列2", "系列3"],
        SeriesData: [820, 932, 901]
      }
    };
  },
  methods: {
    checkMenu(data) {
      console.log(data);
    }
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
