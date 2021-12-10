<template>
  <h3 :style="{ color }">孙子组件: {{ color }}</h3>
</template>

<script lang="ts">
import { inject } from "vue";
export default {
  name: "GrandSon",
  setup() {
    // 注入数据
    const color = inject("color");
    return {
      color,
    };
  },
};
</script>
