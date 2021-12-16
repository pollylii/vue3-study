<template>
  <div class="todo-header">
      <el-input type="text" placeholder="请输入你的任务名，按回车确认" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: "Header",
  components: {},
  setup() {
    return {};
  },
});
</script>
<style scoped>
    .todo-header input{
        outline: none;
    }
</style>
