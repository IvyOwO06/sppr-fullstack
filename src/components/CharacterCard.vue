<script setup>
const props = defineProps({
  name: String,
  status: String,
  species: String,
  image: String,
})

const emit = defineEmits(['interact'])

function interact() {
  emit('interact', props.name)
}
</script>

<template>
  <div class="character-card">
    <img :src="image" :alt="name" class="character-image" />

    <h2>{{ name }}</h2>

    <p>Status: {{ status }}</p>
    <p>Species: {{ species }}</p>

    <button @click="interact">Interact</button>
  </div>
</template>

<style scoped>
.character-card {
  padding: 20px;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 10px;
  text-align: center;
}

.character-image {
  width: 150px;
  height: 150px;
  object-fit: cover;
  border-radius: 8px;
}

.character-card h2 {
  margin: 15px 0 10px;
}

.character-card p {
  margin: 5px 0;
}

button {
  margin-top: 15px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #333;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #555;
}
</style>
