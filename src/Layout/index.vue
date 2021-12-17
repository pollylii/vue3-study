<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <Header :addTodo="addTodo" />
      <List :todos="todos" :deleteTodo="deleteTodo" />
      <Footer />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from "vue";
// 引入子集组件
import Header from "../components/Header.vue";
import List from "../components/List.vue";
import Footer from "../components/Footer.vue";
// 引入接口
import { Todo } from "../types/todo";
export default defineComponent({
  name: "Layout",
  components: { Header, List, Footer },
  setup() {
    const state = reactive<{ todos: Todo[] }>({
      todos: [
        { id: 1, title: "奔驰", isCompleted: false },
        { id: 2, title: "宝马", isCompleted: true },
        { id: 3, title: "奥迪", isCompleted: false },
        { id: 4, title: "拖拉机", isCompleted: false },
      ],
    });
    // 添加数据
    const addTodo = (todo: Todo) => {
      state.todos.unshift(todo);
    };
    // 删除数据
    const  deleteTodo = (index:number) => {
        state.todos.splice(index,1);
    }
    return {
      ...toRefs(state),
      addTodo,
      deleteTodo,
    };
  },
});
</script>
<style scoped>
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  padding: 10px;
  border: 1px solid #dddddd;
  border-radius: 5px;
}
</style>