<template>
  <!-- <div id="center">
    <h2>Jhello polly</h2>
  </div> -->
  <teleport to="#modal">
    <div id="center">
      <h2>Hi Polly</h2>
    </div>
  </teleport >
</template>
<script lang="ts">
export default {};
</script>
<style>
#center {
  width: 200px;
  height: 200px;
  border: 2px solid black;
  background: white;
  position: fixed;
  left: 50%;
  top: 50%;
  margin-left: -100px;
  margin-top: -100px;
}
</style>