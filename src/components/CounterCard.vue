<script setup>
import { ref } from 'vue'

const count = ref(0)

function increaseCount() {
  count.value++
}
</script>

<template>
  <section class="card">
    <h2>Counter</h2>

    <p>You clicked the button {{ count }} times.</p>

    <button @click="increaseCount">+1</button>
  </section>
</template>

<style scoped>
.card {
  padding: 25px;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 10px;
  text-align: center;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>
