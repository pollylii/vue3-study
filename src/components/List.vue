<template>
  <ul class="todo-main">
    <Item v-for="todo in todos" :key="todo.id" :todo="todo" />
  </ul>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Item from "./Item.vue";
export default defineComponent({
  name: "List",
  components: { Item },
  props: ["todos"],
  setup() {
    return {};
  },
});
</script>
<style scoped>
ul {
  margin: 0;
  padding: 0;
}
.todo-main {
  margin-top: 10px;
}
</style>