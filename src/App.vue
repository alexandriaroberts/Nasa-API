<template>
  <div id="app">
    <ScrollUi/>
  </div>
</template>

<script>
import ScrollUi from "./components/ScrollUi.vue";

export default {
  name: "app",
  components: {
    ScrollUi
  }
};
</script>

<style>
html {
  background: #f0cd58; 
  overflow-x: hidden;
  }


</style>
