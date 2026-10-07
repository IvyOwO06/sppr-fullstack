<script setup>
import { ref, onMounted } from 'vue'
import CharacterCard from '@/components/CharacterCard.vue'

const characters = ref([])
const loading = ref(true)
const error = ref('')
const message = ref('Choose a character to interact with!')

function handleInteraction(characterName) {
  message.value = `You interacted with ${characterName}!`
}

async function getCharacters() {
  loading.value = true
  error.value = ''

  try {
    const response = await fetch('https://rickandmortyapi.com/api/character')

    if (!response.ok) {
      throw new Error('Failed to fetch characters')
    }

    const data = await response.json()

    characters.value = data.results
  } catch (err) {
    error.value = 'Something wnet wrong while loading the characters.'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  getCharacters()
})
</script>

<template>
  <main>
    <h1>Characters</h1>

    <p v-if="loading">Loading characters...</p>

    <p v-else-if="error" class="error">
      {{ error }}
    </p>

    <div v-else class="characters">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :name="character.name"
        :status="character.status"
        :species="character.species"
        :image="character.image"
        @interact="handleInteraction"
      />
    </div>

    <p v-if="!loading && !error" class="message">
      {{ message }}
    </p>
  </main>
</template>

<style scoped>
main {
  max-width: 1100px;
  margin: 0 auto;
  padding: 40px 20px;
  text-align: center;
}

.characters {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-top: 30px;
}

.message {
  margin-top: 30px;
}

.error {
  color: #d00000;
  font-weight: bold;
}

@media (max-width: 700px) {
  .characters {
    grid-template-columns: 1fr;
  }
}
</style>
