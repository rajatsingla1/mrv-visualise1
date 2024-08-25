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
          left: "2%",
          right: "2%",
          top: "20%",
          bottom: "8%",
          symbol: "emptyCircle",
          orient: "BT",
          initialTreeDepth: 3,
          expandAndCollapse: true,
          label: {
            position: "bottom",
            rotate: 90,
            verticalAlign: "middle",
            align: "right",
            formatter: (params: any) =>
              params.name.length > 24
                ? params.name.substring(0, 24) + ".."
                : params.name,
          },
          leaves: {
            label: {
              position: "top",
              rotate: 90,
              verticalAlign: "middle",
              align: "left",
            },
          },
          emphasis: {
            focus: "descendant",
          },
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
  height: 180vh;

  padding: 2rem;
}
</style>
