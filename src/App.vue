<template>
  <div id="app">
    <List></List>
  </div>
</template>

<script>
import List from "./components/List.vue";

export default {
  name: "App",
  data() {},
  components: {
    List
  }
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}
body {
  background-color: hsl(100, 10, 5);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: hsl(100, 0, 75);
  margin-top: 6vh;
  display: flex;
  justify-content: center;
}
</style>
