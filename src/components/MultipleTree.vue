<template>
  <div
    v-for="tr in activeTree"
    :key="tr.id"
    :id="`main-${tr.id}`"
    class="main"
  ></div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import * as echarts from "echarts";
import { mrvData } from "../data/mrv";

const activeTree: any = ref([]);
mrvData.forEach((element, index) => {
  activeTree.value.push({
    name: element.name,
    id: index + 1,
    data: element,
  });
});

onMounted(() => {
  activeTree.value.forEach((element: any) => {
    var chartDom = document.getElementById(`main-${element.id}`);
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
        series: {
          type: "tree",
          name: element.name,
          data: [element.data],

          symbolSize: 7,
          emphasis: {
            focus: "descendant",
          },
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
          expandAndCollapse: true,
          animationDuration: 550,
          animationDurationUpdate: 750,
        },
      })
    );

    option && myChart.setOption(option);
  });
});
</script>
<style scoped>
.main {
  width: 90%;
  height: 60vh;
  padding: 2rem;
}
</style>
