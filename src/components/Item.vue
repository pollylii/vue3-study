<template>
  <li>
      <label>
          <el-checkbox></el-checkbox>
          <span>xxxx</span>
      </label>
      <el-button class="btn" size="mini" type="">删除</el-button>
  </li>
 
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: "Item",
  components: {},
  setup() {
    return {};
  },
});
</script>
<style scoped>
    li{
        list-style:none;
        /*cursor: pointer;*/
        height: 36px;
        line-height: 36px;
        border-bottom: 1px solid #dddddd;
    }
    li label{
        float: left;
        cursor: pointer;
    }
    li:before{
        content: inherit;
    }
    li .btn{
        float: right;
        /*display: none;*/
        margin-top: 3px;
    }
    li .btn:hover{
        display: block;
    }
    li label li input{
        vertical-align: middle;
        position: relative;
        top: -1px;
    }
</style>

