<script setup>
import CounterCard from '../components/CounterCard.vue'
</script>

<template>
  <main>
    <h1>* Welcome to the Dark World!</h1>

    <p>This is my Vue application inspired by Undertale and Deltarune.</p>

    <CounterCard />
  </main>
</template>

<style scoped>
main {
  text-align: center;
  padding: 40px 20px;
}

h1 {
  margin-bottom: 20px;
}

p {
  margin-bottom: 30px;
}
</style>
