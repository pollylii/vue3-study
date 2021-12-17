<template>
  <div class="todo-footer">
    <label>
      <el-checkbox v-model="isCompleteAll"></el-checkbox>
    </label>
    <span>
      <span>已完成 {{ count }}</span>
      <span>/全部 {{ todos.length }}</span>
    </span>
    <el-button class="btn" size="mini" type="danger" @click="clearCompletedAll">清除已完成任务</el-button>
  </div>
</template>

<script lang="ts">
import { defineComponent,computed } from "vue";
import { Todo } from "../types/todo";
export default defineComponent({
  name: "Footer",
  components: {},
  props: {
    todos: {
      type: Array as () => Todo[],
      required: true,
    },
    checkAll: {
      type: Function,
      required: true,
    },
    clearCompletedAll: {
      type: Function,
      required: true,
    },
  },

  setup(props) {
    //   已完成的计算属性操作
    const count = computed(()=>{
      return props.todos.reduce((pre,todo) => pre+(todo.isCompleted?1:0), 0);
    });
    // 全选/全不选 的计算属性
    const isCompleteAll = computed({
      get() {
        return count.value > 0 && props.todos.length === count.value;
      },
      set(val) {
          props.checkAll(val)
      },
    });
    return {
      count,
      isCompleteAll,
    };
  },
});
</script>
<style scoped>
.todo-footer {
  margin-top: 5px;
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
}
.todo-footer label {
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
