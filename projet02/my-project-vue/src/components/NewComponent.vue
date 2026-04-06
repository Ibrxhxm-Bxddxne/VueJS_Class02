<template>
  <div class="new-component">
    <h2>{{ title }}</h2>
    <p>{{ message }}</p>

    <button @click="changeMessage">
      Cliquer ici
    </button>
  </div>
</template>

<script>
export default {
  name: "NewComponent",
  data() {
    return {
      title: "Mon Nouveau Composant",
      message: "Bonjour depuis Vue.js 👋"
    };
  },
  methods: {
    changeMessage() {
      this.message = "Le message a été changé ! 🎉";
    }
  }
};
</script>

<style scoped>
.new-component {
  border: 2px solid #42b983;
  padding: 15px;
  border-radius: 8px;
  text-align: center;
}

button {
  margin-top: 10px;
  padding: 8px 12px;
  background-color: #42b983;
  border: none;
  color: white;
  cursor: pointer;
  border-radius: 4px;
}

button:hover {
  background-color: #369870;
}
</style>