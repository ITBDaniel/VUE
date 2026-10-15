<script setup>
import { ref, computed } from 'vue'
// Dades reactives
const preu = ref(100)
const descompte = ref(10) // en percentatge
// Propietat calculada: calcula el preu final automàticament
const preuFinal = computed(() => {
  const total = preu.value - (preu.value * descompte.value / 100)
  return total.toFixed(2)
})
// Propietat calculada: missatge personalitzat segons el descompte
const missatgeDescompte = computed(() => {
  if (descompte.value === 0) return 'Sense descompte aplicat'
  if (descompte.value < 20) return 'Petit descompte'
  return 'Gran descompte!'
})
</script>
<template>
  <div class="p-4">
    <h2>Calculadora de descompte</h2>
    <label>
      Preu original:
      <input type="number" v-model="preu" /> €
    </label>
    <br />
    <label>
      Descompte:
      <input type="number" v-model="descompte" /> %
    </label>
    <hr />
    <p>Preu final: <strong>{{ preuFinal }}</strong> €</p>
    <p>{{ missatgeDescompte }}</p>
  </div>
</template>