<script setup>
import Header from './components/header.vue'
import CounterCard from './components/CounterCard.vue'
import InfoCard from './components/InfoCard.vue'
</script>

<template>
  <Header />

  <main>
    <CounterCard />

    <InfoCard />
    <InfoCard />
  </main>
</template>

<style scoped>
main {
  max-width: 800px;
  margin: 40px auto;
  padding: 0 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
