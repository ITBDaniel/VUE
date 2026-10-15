<script setup>
import { ref } from 'vue'

// Definim un objecte reactiu
const usuari = ref({
  nom: 'Anna',
  edat: 25
})

// Funció que modifica una propietat
const augmentarEdat = () => {
  usuari.value.edat++
}
</script>

<template>
  <div>
    <p>Nom: {{ usuari.nom }}</p>
    <p>Edat: {{ usuari.edat }}</p>
    <button @click="augmentarEdat">Augmenta l'edat</button>
  </div>
</template>