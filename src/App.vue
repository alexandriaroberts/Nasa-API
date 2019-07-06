<template>
  <div id="app">
    <Search />
  </div>
</template>

<script>
import Search from "./components/Search";

export default {
  name: "App",
  components: {
    Search
  }
};
</script>

<style>
:root {
  --color: #ffffff;
  --main-bg-color: #141412;
  --spacing: 2rem;
}
html {
  background-color: var(--main-bg-color);
  overflow-x: hidden;
}
</style>
