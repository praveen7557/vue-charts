<template>
  <div id="app">
    <div class="line chart">
      <line-chart :style="myStyles" :options="options"/>
    </div>
    <!-- <div class="line chart">
      <bar :style="myStyles" :options="options" />
    </div>-->
    <!-- <div class="line chart">
      <floating-bar :style="myStyles" :options="options" />
    </div>-->
    <div class="line chart">
      <stacked-bar :style="myStyles" :options="options"/>
    </div>
  </div>
</template>

<script>
import LineChart from "./components/Line";
import FloatingBar from "./components/FloatingBar";
import Bar from "./components/Bar";
import StackedBar from "./components/StackedBar";

export default {
  name: "App",
  components: {
    LineChart,
    Bar,
    FloatingBar,
    StackedBar
  },
  data() {
    return {
      myStyles: {
        height: "100%",
        width: "100%",
        position: "relative"
      },
      options: {
        // cornerRadius: 4,
        responsive: true,
        maintainAspectRatio: false
      }
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.chart {
  height: 300px;
}
</style>
