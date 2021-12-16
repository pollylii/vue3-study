<template>
  <ul class="todo-main">
      <Item />
  </ul>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import Item from './Item.vue'
export default defineComponent({
  name: "List",
  components: { Item },
  setup() {
    return {};
  },
});
</script>
<style scoped>
  ul{
      margin: 0;
      padding: 0;
  }
  .todo-main{
      margin-top: 10px;
  }
</style>