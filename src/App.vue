<template>
  <div>
    <!-- <HelloWorld /> -->
    <!-- <modal /> -->
    <Suspense>
      <template #default>
        <!-- <AsyncShow /> -->
        <girl-show />
      </template>
      <template #fallback>
        <h1>Loading...</h1>
      </template>
    </Suspense>
  </div>
</template>

<script lang="ts">
import { ref, onErrorCaptured } from "vue";
// import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
// import modal from "./components/Modal.vue";
// import useUrlAxios from "./hooks/useUrlAxios";
// import AsyncShow from "./components/AsyncShow.vue";
import GirlShow from "./components/GirlShow.vue";

export default {
  name: "App",
  components: {
    // HelloWorld,
    // modal,
    // AsyncShow,
    GirlShow,
  },
  setup() {
    onErrorCaptured((error) => {
      console.log(`error====>`, error);
      return true;
    });
    return {};
  },
};
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
}
</style>
