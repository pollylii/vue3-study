<template>
  <div class="todo-footer">
        <label>
            <el-checkbox  ></el-checkbox>
        </label>
        <span>
            <span>已完成</span>
            <span>/全部</span>
        </span>
       <el-button class="btn" size="mini" type="danger">清除已完成任务</el-button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: "Footer",
  components: {},
  setup() {
    return {};
  },
});
</script>
<style scoped>
    .todo-footer{
        margin-top: 5px;
        height: 40px;
        line-height: 40px;
        padding-left: 6px;
    }
    .todo-footer label{
        display: inline-block;
        cursor: pointer;
        margin-right: 20px;
    }
    .todo-footer label input {
        position: relative;
        top: -1px;
        vertical-align: middle;
        margin-right: 5px;
    }
    .todo-footer .btn {
        float: right;
        margin-top: 5px;
    }
</style>
