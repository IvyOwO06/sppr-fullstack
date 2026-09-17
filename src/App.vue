<script setup>
import { ref } from 'vue'

const name = ref('Ivy')
const count = ref(0)

function increaseCount() {
  count.value++
}
</script>

<template>
  <main>
    <h1>My Vue Website</h1>

    <p>Hello, {{ name }}!</p>

    <p>Button clicked: {{ count }} times</p>

    <button @click="increaseCount">Click me</button>
  </main>
</template>

<style scoped>
main {
  max-width: 800px;
  margin: 50px auto;
  text-align: center;
  font-family: Arial, sans-serif;
}

h1 {
  font-size: 40px;
}

p {
  font-size: 20px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>
