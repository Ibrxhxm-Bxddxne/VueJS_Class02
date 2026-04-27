<script setup>
import { ref, reactive, computed } from 'vue'

// Variables
const product = ref('Pizza')
const type = ref('Orientale')
const price = ref(12)

const image = ref(
  new URL('./assets/images/pizza1-tomate.jpg', import.meta.url).href
)

const sale = ref(true)
const notAvailable = ref(true)

const ingredients = ref([
  "Olives",
  "Poulet roti",
  "Bacon",
  "Poivrons",
  "Champignons",
  "Mozzarella",
  "Oeuf"
])

const sauces = ref([
  {
    id: 1001,
    type: "Sauce Tomate",
    color: "#db4006",
    image: new URL('./assets/images/pizza1-tomate.jpg', import.meta.url).href,
  },
  {
    id: 1002,
    type: "Crème Fraiche",
    color: "#e9cb8f",
    image: new URL('./assets/images/pizza1-creme.jpg', import.meta.url).href,
  }
])

const energy = reactive({
  Kcal: 242,
  Glucides: 27.99,
  Fibres: 1.75,
  Proteines: 9.62,
  Sel: 11
})

const totalePrice = ref(0)
const nbrProduct = ref(0)
const promo = ref('')

// Computed
const title = computed(() => product.value + ' ' + type.value)

// Fonctions
function addProduct() {
  nbrProduct.value++
  totalePrice.value = nbrProduct.value * price.value

  if (promo.value === 'royale') {
    totalePrice.value *= 0.8 // réduction 20%
  }
}

function updateImage(newImage) {
  image.value = newImage
}
</script>

<template>
  <div style="padding: 20px; font-family: Arial">

    <!-- Titre -->
    <h1>{{ title }}</h1>

    <!-- Image -->
    <img :src="image" width="300" />

    <!-- Indisponible -->
    <p v-if="notAvailable" style="color:red">
      Momentanément indisponible
    </p>

    <!-- Prix -->
    <p v-if="sale" style="color:green">
      Prix promo : {{ price }} €
    </p>
    <p v-else>
      Prix : {{ price }} €
    </p>

    <!-- Ingrédients -->
    <h3>Ingrédients :</h3>
    <ul>
      <li v-for="item in ingredients" :key="item">
        {{ item }}
      </li>
    </ul>

    <!-- Sauces -->
    <h3>Sauces :</h3>
    <div style="display:flex; gap:10px;">
      <span
        v-for="sauce in sauces"
        :key="sauce.id"
        @mouseover="updateImage(sauce.image)"
        :style="{
          backgroundColor: sauce.color,
          padding: '10px',
          cursor: 'pointer',
          color: '#fff'
        }"
      >
        {{ sauce.type }}
      </span>
    </div>

    <!-- Valeurs nutritionnelles -->
    <h3>Valeurs nutritionnelles :</h3>
    <ul>
      <li>Kcal: {{ energy.Kcal }}</li>
      <li>Glucides: {{ energy.Glucides }}</li>
      <li>Fibres: {{ energy.Fibres }}</li>
      <li>Protéines: {{ energy.Proteines }}</li>
      <li>Sel: {{ energy.Sel }}</li>
    </ul>

    <!-- Code promo -->
    <input v-model="promo" placeholder="Code promo" />

    <!-- Bouton -->
    <br /><br />
    <button @click="addProduct">
      Ajouter au panier
    </button>

    <!-- Résultat -->
    <p>Nombre de produits : {{ nbrProduct }}</p>
    <p>Total à payer : {{ totalePrice.toFixed(2) }} €</p>

  </div>
</template>