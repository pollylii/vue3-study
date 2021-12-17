<template>
  <li>
    <el-checkbox :label="todo.title"></el-checkbox>
    <el-button class="btn" size="mini" type="">删除</el-button>
  </li>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";
import { Todo } from "../types/todo";
export default defineComponent({
  name: "Item",
  components: {},
  props: {
    todo: Object as () => Todo, // 函数返回的是Todo类型
  },
  setup(props) {
    console.log(78789787878978, props.todo);
    return {};
  },
});
</script>
<style scoped>
li {
  list-style: none;
  /*cursor: pointer;*/
  height: 36px;
  line-height: 36px;
  border-bottom: 1px solid #dddddd;
}
li label {
  float: left;
  cursor: pointer;
}
li:before {
  content: inherit;
}
li .btn {
  float: right;
  /*display: none;*/
  margin-top: 3px;
}
li .btn:hover {
  display: block;
}
li label li input {
  vertical-align: middle;
  position: relative;
  top: -1px;
}
</style>

