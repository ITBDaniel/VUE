<script setup>
import { ref, computed } from 'vue'
// Dades reactives
const nombre = ref('Joan')
  // Propietat calculada per convertir el nom a majúscules
const nomMajuscules = computed(() => nombre.value.toUpperCase())
</script>
<template>
  <div>
    <p>Nombre: {{ nombre }}</p>
    <p>Nom en majúscules (computed): {{ nomMajuscules }}</p>
  </div>
</template>