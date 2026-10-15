<template>
  <div>
    <h1 v-bind:title="titol">Passa el ratolí per aquest text</h1>
    <img :src="imatgeUrl" alt="Imatge dinàmica" />
  </div>
</template>

<script setup>
const titol = 'Hola, aquest és el títol dinàmic!'
const imatgeUrl = 'https://www.shutterstock.com/image-illustration/'
</script>