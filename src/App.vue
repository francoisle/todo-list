<template>
  <div id="app">
    <TodoList msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "app",
  components: {
    TodoList
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 60px;
  margin-left: auto;
  margin-right: auto;
  max-width: 500px;
  min-width: 300px;
  line-height: 24px;
  font-size: 16px;
  box-sizing: border-box;
}
</style>
