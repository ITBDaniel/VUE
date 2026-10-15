<script setup>
import { ref } from 'vue'
const missatge = ref('Hola, món!')
const canviarMissatge = () => {
  missatge.value = 'Hola, Vue!'
}
</script>

<template>
  <div>
    <h1>{{ missatge }}</h1>
    <button @click="canviarMissatge">Canvia el missatge</button>
  </div>
</template>

<style scoped>
div {
  text-align: center;
}
button {
  margin-top: 10px;
}
</style>
