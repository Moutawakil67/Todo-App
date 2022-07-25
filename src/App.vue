<template>
  <div id="App"></div>
  <calculatrice />
</template>

<script>
import calculatrice from "./components/calculatrice.vue";

export default {
  name: "App",
  components: {
    calculatrice,
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
