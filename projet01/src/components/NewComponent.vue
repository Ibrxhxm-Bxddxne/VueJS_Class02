<template>
  <div>
    <p>{{ message }}</p>
    <button @click="showAlert()">Click me</button>
  </div>
</template>

<script>
export default {
  name: "NewComponent",

  data() {
    return {
      message: "Hello from New Component!"
    };
  },

  methods: {
    showAlert() {
      alert(this.message);
    }
  }
};
</script>

<style scoped>
button {
  padding: 10px;
  background-color: #42b983;
  color: white;
  border: none;
}
</style>