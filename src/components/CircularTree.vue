<template>
  <div id="main"></div>
</template>

<script setup lang="ts">
import { onMounted } from "vue";
import * as echarts from "echarts";
import { mrvData } from "../data/mrv";

const data = {
  name: "",
  children: mrvData,
};

onMounted(() => {
  var chartDom = document.getElementById("main");
  var myChart = echarts.init(chartDom);
  var option;

  myChart.showLoading();
  myChart.hideLoading();
  myChart.setOption(
    (option = {
      tooltip: {
        trigger: "item",
        triggerOn: "mousemove",
      },
      series: [
        {
          type: "tree",
          data: [data],
          layout: "radial",

          symbol: "emptyCircle",
          symbolSize: 7,
          initialTreeDepth: 3,
          animationDurationUpdate: 750,
          emphasis: {
            focus: "descendant",
          },

          label: {
            formatter: (params: any) =>
              params.name.length > 24
                ? params.name.substring(0, 24) + ".."
                : params.name,
          },
        },
      ],
    })
  );

  option && myChart.setOption(option);
});
</script>
<style scoped>
#main {
  width: 98%;
  height: 160vh;

  padding: 2rem;
}
</style>
