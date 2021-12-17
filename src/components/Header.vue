<template>
  <div class="todo-header">
    <el-input
      type="text"
      placeholder="请输入你的任务名，按回车确认"
      @keyup.enter="add"
      v-model="title"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "Header",
  components: {},
  props: {
    addTodo: {
      type: Function,
      required: true,
    },
  },
  setup(props) {
    const title = ref("");
    const add = () => {
      //获取文本框输入数据
      const text = title.value;
      if (!text.trim()) return;
      const todo = {
        id: Date.now(),
        title: text,
        isCompleted: false,
      };
      props.addTodo(todo);
      // 清空文本框
      title.value = "";
    };

    return {
      title,
      add,
    };
  },
});
</script>
<style scoped>
.todo-header input {
  outline: none;
}
</style>
