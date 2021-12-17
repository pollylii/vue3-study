<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <Header :addTodo="addTodo" />
      <List :todos="todos" :deleteTodo="deleteTodo" :updateTodo="updateTodo" />
      <Footer
        :todos="todos"
        :checkAll="checkAll"
        :clearCompletedAll="clearCompletedAll"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, reactive, toRefs, watch } from "vue";
// 引入子集组件
import Header from "../components/Header.vue";
import List from "../components/List.vue";
import Footer from "../components/Footer.vue";
// 引入接口
import { Todo } from "../types/todo";
import { saveTodos, readTodos } from "../utils/localStorageUtils";
export default defineComponent({
  name: "Layout",
  components: { Header, List, Footer },
  setup() {
    // 定义一组数据
    const state = reactive<{ todos: Todo[] }>({
      todos: [],
    });
    onMounted(()=>{
      setTimeout(()=>{
        state.todos = readTodos()
      },2000)
    })
    // const state = reactive<{ todos: Todo[] }>({
    //   todos: [
    //     { id: 1, title: "奔驰", isCompleted: false },
    //     { id: 2, title: "宝马", isCompleted: true },
    //     { id: 3, title: "奥迪", isCompleted: false },
    //     { id: 4, title: "拖拉机", isCompleted: false },
    //   ],
    // });
    // 添加数据
    const addTodo = (todo: Todo) => {
      state.todos.unshift(todo);
    };
    // 删除数据
    const deleteTodo = (index: number) => {
      state.todos.splice(index, 1);
    };
    // 修改todo的isCompleted属性状态
    const updateTodo = (todo: Todo, isCompleted: boolean) => {
      todo.isCompleted = isCompleted;
    };
    //全选/全不选 操作
    const checkAll = (isCompleted: boolean) => {
      //遍历数组
      state.todos.forEach((todo) => {
        todo.isCompleted = isCompleted;
      });
    };
    //清理左右选中的数据
    const clearCompletedAll = () => {
      state.todos = state.todos.filter((todo) => !todo.isCompleted);
    };
    // watch(()=>state.todos,(value)=>{
    //   localStorage.setItem('todos_key', JSON.stringify(value))

    // },{deep:true})
    watch(() => state.todos, saveTodos, { deep: true });
    return {
      ...toRefs(state),
      addTodo,
      deleteTodo,
      updateTodo,
      checkAll,
      clearCompletedAll,
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