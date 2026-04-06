<template>
  <div id="app">
    <h1>Bienvenue dans mon app Vue 🚀</h1>
    <NewComponent />
  </div>
</template>

<script>
import NewComponent from "./components/NewComponent.vue";

export default {
  name: "App",
  components: {
    NewComponent
  }
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 50px;
}
</style>