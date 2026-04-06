<script>
export default {
  data() {
    return {
      product: 'Pizza',
      type: 'Orientale',
      price: 12,
      image: "assets/images/pizza1-tomate.jpg",
      sale: true,
      notAvailable: true,
      ingrediants: [
        "Olives", "Poulet roti", "Bacon",
        "Poivrons", "Champignons", "Mozzarella", "Oeuf"
      ],
      sauces: [
        {
          id: 1001,
          type: "Sauce Tomate",
          color: "#db4006",
          image: "assets/images/pizza1-tomate.jpg",
        },
        {
          id: 1002,
          type: "Crème Fraiche",
          color: "#e9cb8f",
          image: "assets/images/pizza1-creme.jpg",
        },
      ],
      energy: {
        Kcal: 242,
        Glucides: 27.99,
        Fibres: 1.75,
        Proteines: 9.62,
        Sel: 11
      },
      totalePrice: 0,
      nbrProduct: 0,
      promo: ''
    }
  },

  computed: {
    title() {
      return this.product + " " + this.type
    }
  },

  methods: {
    addProduct() {
      this.nbrProduct++
      this.totalePrice = this.nbrProduct * this.price

      if (this.promo === 'royale') {
        this.totalePrice *= 0.8 // réduction 20%
      }
    },

    updateImage(newImage) {
      this.image = newImage
    }
  }
}
</script>

<template>
  <div id="app">

    <!-- Titre -->
    <h1>{{ title }}</h1>

    <!-- Image -->
    <img :src="image" width="300">

    <!-- Disponibilité -->
    <p v-if="notAvailable">Momentanément indisponible</p>

    <!-- Prix -->
    <p v-if="sale">Prix promo : {{ price }} €</p>
    <p v-else>Prix : {{ price }} €</p>

    <!-- Ingrédients -->
    <h3>Ingrédients :</h3>
    <ul>
      <li v-for="(item, index) in ingrediants" :key="index">
        {{ item }}
      </li>
    </ul>

    <!-- Sauces -->
    <h3>Sauces :</h3>
    <div v-for="sauce in sauces" :key="sauce.id">
      <p 
        @mouseover="updateImage(sauce.image)"
        :style="{ backgroundColor: sauce.color }"
      >
        {{ sauce.type }}
      </p>
    </div>

    <!-- Valeurs nutritionnelles -->
    <h3>Valeurs nutritionnelles :</h3>
    <ul>
      <li v-for="(value, key) in energy" :key="key">
        {{ key }} : {{ value }}
      </li>
    </ul>

    <!-- Promo -->
    <input v-model="promo" placeholder="Code promo">

    <!-- Bouton -->
    <button @click="addProduct">Ajouter</button>

    <!-- Résultat -->
    <p>Quantité : {{ nbrProduct }}</p>
    <p>Total : {{ totalePrice }} €</p>

  </div>
</template>