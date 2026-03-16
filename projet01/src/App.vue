<template>
  <div>
    <h1>Welcome to Vue 3</h1>
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