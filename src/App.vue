<template>
  <div id="App"></div>
  <todo />
</template>

<script>
import todo from "./components/todo.vue";

export default {
  name: "App",
  components: {
    todo,
  },
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

h1 {
  color: blue;
}
</style>
