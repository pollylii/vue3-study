<template>
  <div class="m-a">
    <div>
      <button
        v-for="(item, index) in nums"
        v-bind:key="index"
        @click="numFun(index)"
      >
        {{ item }}
      </button>
    </div>
    <div>你选择了【{{ num }}】</div>
  </div>

  <div class="m-a">
    <div><button @click="overAction">点餐完毕</button></div>
    <div>{{ overText }}</div>
  </div>

  <!-- 使用时间工具组件 -->
  <div class="m-a">
    <div>{{ nowTime }}</div>
    <div><button @click="getNowTime">显示时间</button></div>
  </div>

  <!-- 使用axios -->
  <div class="m-a">
    <div v-if="loading">Loading.....</div>
    <img
      v-if="loaded"
      :src="result.message"
      style="max-width: 200px; max-height: 200px"
    />
  </div>
</template>

<script lang="ts">
import { ref, reactive, toRefs, watch } from "vue";
import { nowTime, getNowTime } from "../hooks/useNowTime";
import useUrlAxios from "../hooks/useURLAxios";

// 自定义一个类型
interface dataType {
  nums: string[];
  num: string;
  numFun: (index: number) => void;
}
export default {
  name: "HelloWorld",
  setup() {
    const data: dataType = reactive({
      nums: ["第一", "第二", "第三"],
      num: "",
      numFun: (index: number) => {
        data.num = data.nums[index];
      },
    });
    const refData = toRefs(data);

    const overText = ref("红浪漫");
    const overAction = () => {
      overText.value = overText.value + "点餐完成 | ";
      // document.title = overText.value;
    };
    watch(
      [
        overText,
        () => {
          data.num;
        },
      ],
      (newValue, oldValue) => {
        console.log(`new===>, ${newValue}`);
        console.log(`old===>, ${oldValue}`);
        document.title = newValue[0];
      }
    );

    const { result, loading, loaded } = useUrlAxios(
      "https://dog.ceo/api/breeds/image/random"
    );
    return {
      ...refData,
      overText,
      overAction,
      nowTime,
      getNowTime,
      result,
      loading,
      loaded,
    };
  },
};
</script>

<style scoped>
.m-a {
  margin: auto;
  margin-bottom: 20px;
}
</style>
