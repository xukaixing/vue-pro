<template>
  <div id="app">
    <app01></app01>
    <div>---------------------------------------------</div>
    <app02></app02>
    <div>---------------------------------------------</div>
    <app03></app03>
    <div>---------------------------------------------</div>
    <app04></app04>
    <div>---------------------------------------------</div>
    <app05></app05>
    <div>---------------------------------------------</div>
    <app06></app06>
  </div>
</template>

<script>
// @默认代表src，在webpack.base.conf中定义alias别名
import app01 from "@/components/App01";
import app02 from "@/components/App02";
import app03 from "@/components/App03";
import app04 from "@/components/App04";
import app05 from "@/components/App05";
import app06 from "@/components/App06";

export default {
  name: "App",
  // 局部注册组件
  components: {
    app01,
    app02,
    app03,
    app04,
    app05,
    app06,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin: 10px;
}
.header-title {
  color: #da1f1f;
}
</style>