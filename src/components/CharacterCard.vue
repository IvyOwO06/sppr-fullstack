<script setup>
defineProps({
  name: String,
  hp: Number,
})

const emit = defineEmits(['interact'])

function interact() {
  emit('interact', name)
}
</script>

<template>
  <div class="character-card">
    <h2>{{ name }}</h2>

    <p>HP: {{ hp }}</p>

    <button @click="interact">Interact</button>
  </div>
</template>

<style scoped>
.character-card {
  border: 2px solid white;
  padding: 20px;
  background-color: black;
  color: white;
  text-align: center;
}

.character-card h2 {
  margin-top: 0;
}

button {
  background-color: black;
  color: white;
  border: 2px solid white;
  padding: 10px 20px;
  cursor: pointer;
}

button:hover {
  background-color: white;
  color: black;
}
</style>
