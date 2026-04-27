<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      appName: 'TP Axios Vue.js',
      posts: [], // Liste des posts
      selectedPost: null, // Post sélectionné individuellement
      postIdToFetch: 1, // ID lié au v-model de l'input
      isLoadingList: false,
      isLoadingSingle: false,
      errorList: null,
      errorSingle: null,
    };
  },
  methods: {
    // ÉTAPE 4 : Récupérer tous les posts
    async fetchAllPosts() {
      this.isLoadingList = true;
      this.errorList = null;
      this.posts = [];
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts');
        this.posts = response.data;
      } catch (error) {
        if (error.response) {
          this.errorList = `Erreur ${error.response.status}: ${error.response.statusText}`;
        } else {
          this.errorList = "Impossible de contacter le serveur.";
        }
      } finally {
        this.isLoadingList = false;
      }
    },

    // ÉTAPE 5 : Récupérer un post spécifique
    async fetchSinglePost() {
      if (!this.postIdToFetch || this.postIdToFetch < 1) {
        this.errorSingle = "Veuillez entrer un ID valide.";
        this.selectedPost = null;
        return;
      }

      this.isLoadingSingle = true;
      this.errorSingle = null;
      this.selectedPost = null;

      try {
        const url = `https://jsonplaceholder.typicode.com/posts/${this.postIdToFetch}`;
        const response = await axios.get(url);
        this.selectedPost = response.data;
      } catch (error) {
        if (error.response && error.response.status === 404) {
          this.errorSingle = `Le post ${this.postIdToFetch} n'existe pas (404).`;
        } else {
          this.errorSingle = "Erreur lors de la récupération du post.";
        }
      } finally {
        this.isLoadingSingle = false;
      }
    }
  },
  mounted() {
    // Chargement automatique au démarrage
    this.fetchAllPosts();
  }
}
</script>

<template>
  <div id="app">
    <header>
      <h1>{{ appName }}</h1>
    </header>

    <main>
      <section class="posts-list">
        <h2>Liste des Posts</h2>
        <button @click="fetchAllPosts" :disabled="isLoadingList">
          {{ isLoadingList ? 'Chargement...' : 'Charger tous les Posts' }}
        </button>

        <p v-if="isLoadingList" class="loading">Chargement de la liste...</p>
        <p v-if="errorList" class="error">{{ errorList }}</p>

        <ul v-if="posts.length > 0 && !isLoadingList">
          <li v-for="post in posts.slice(0, 10)" :key="post.id"> <h3>{{ post.id }}. {{ post.title }}</h3>
            <p>{{ post.body.substring(0, 100) }}...</p>
          </li>
        </ul>
      </section>

      <hr>

      <section class="single-post">
        <h2>Détail d'un Post</h2>
        <div class="controls">
          <label for="postId">ID du Post : </label>
          <input type="number" id="postId" v-model.number="postIdToFetch" min="1">
          <button @click="fetchSinglePost" :disabled="isLoadingSingle">
            {{ isLoadingSingle ? 'Chargement...' : 'Charger le Post' }}
          </button>
        </div>

        <p v-if="isLoadingSingle" class="loading">Chargement du post...</p>
        <p v-if="errorSingle" class="error">{{ errorSingle }}</p>

        <article v-if="selectedPost && !isLoadingSingle">
          <h3>{{ selectedPost.id }}. {{ selectedPost.title }}</h3>
          <p>{{ selectedPost.body }}</p>
          <p><em>User ID: {{ selectedPost.userId }}</em></p>
        </article>
      </section>
    </main>
  </div>
</template>

<style>
/* (Le CSS reste le même que celui fourni dans votre énoncé) */
</style>
