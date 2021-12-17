<template>
  <li
    @mouseenter="mouseHandler(true)"
    @mouseleave="mouseHandler(false)"
    :style="{ backgroundColor: bgColor, color: myColor }"
  >
    <el-checkbox :label="todo.title" v-model="isComplete"></el-checkbox>
    <el-button size="mini" type="danger" v-show="isBtnShow" @click="delTodo"
      >删除</el-button
    >
  </li>
</template>

<script lang="ts">
import { defineComponent, reactive, ref,computed } from "vue";
import { ElMessageBox, ElMessage } from "element-plus";
import { Todo } from "../types/todo";
export default defineComponent({
  name: "Item",
  components: {},
  props: {
    todo: {
      type: Object as () => Todo, // 函数返回的是Todo类型
      required: true,
    },
    deleteTodo: {
      type: Function,
      required: true,
    },
    updateTodo: {
      type: Function,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  setup(props) {
    // 背景色
    const bgColor = ref("white");
    // 前景色
    const myColor = ref("black");
    // 设置删除按钮默认不显示
    const isBtnShow = ref(false);
    // 鼠标进入事件和离开事件的回调函数
    const mouseHandler = (flag: boolean) => {
      if (flag) {
        // 鼠标进入
        bgColor.value = "pink";
        myColor.value = "green";
        isBtnShow.value = true;
      } else {
        // 鼠标出去
        bgColor.value = "white";
        myColor.value = "black";
        isBtnShow.value = false;
      }
    };
    //删除数据
    const delTodo = () => {
      ElMessageBox.confirm("确定删除吗?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "关闭",
        type: "warning",
      })
        .then(() => {
          props.deleteTodo(props.index);
          ElMessage({
            type: "success",
            message: "删除成功！",
          });
        })
        .catch(() => {
          ElMessage({
            type: "info",
            message: "取消删除！",
          });
        });
    };
    // 计算属性的方式----让当前的复选框选中/不选中
    const isComplete = computed({
        get(){
            return props.todo.isCompleted
        },
        set(val){
            // todo对象中的isCompleted属性操作
            props.updateTodo(props.todo, val)
        }
    })
    return {
      mouseHandler,
      bgColor,
      myColor,
      isBtnShow,
      delTodo,
      isComplete,
    };
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

li:before {
  content: inherit;
}
li .el-button {
  float: right;
  /* display: none; */
  margin-top: 3px;
}
li label li input {
  vertical-align: middle;
  position: relative;
  top: -1px;
}
</style>

