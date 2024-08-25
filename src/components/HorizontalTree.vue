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
          top: "1%",
          left: "7%",
          bottom: "1%",
          right: "20%",
          symbolSize: 7,
          initialTreeDepth: 3,
          label: {
            position: "left",
            verticalAlign: "middle",
            align: "right",

            formatter: (params: any) =>
              params.name.length > 28
                ? params.name.substring(0, 28) + ".."
                : params.name,
          },
          leaves: {
            label: {
              position: "right",
              verticalAlign: "middle",
              align: "left",
            },
          },
          emphasis: {
            focus: "descendant",
          },
          expandAndCollapse: true,
          animationDuration: 550,
          animationDurationUpdate: 750,
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
  height: 220vh;

  padding: 2rem;
}
</style>
