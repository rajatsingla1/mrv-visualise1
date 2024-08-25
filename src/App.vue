<template>
  <div class="container">
    <div class="selectBox">
      <select v-model="treeType">
        <option></option>
        <option>circular</option>
        <option>horizontal</option>
        <option>multiple</option>
        <option>vertical</option>
      </select>
    </div>
    <div>
      <CircularTree v-if="treeType == 'circular'" />
      <HorizontalTree v-if="treeType == 'horizontal'" />
      <MultipleTree v-if="treeType == 'multiple'" />
      <VerticalTree v-if="treeType == 'vertical'" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import CircularTree from "./components/CircularTree.vue";
import HorizontalTree from "./components/HorizontalTree.vue";
import MultipleTree from "./components/MultipleTree.vue";
import VerticalTree from "./components/VerticalTree.vue";

const treeType = ref("multiple");
</script>

<style>
.container {
  margin: 2rem 2rem;
}
select {
  width: 120px;
  height: 32px;
  padding: 3px;
}
</style>
