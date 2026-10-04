<script setup>
import { ref } from 'vue'
import CharacterCard from '@/components/CharacterCard.vue'

const message = ref('Choose a character to interact with!')

function handleInteraction(characterName) {
  message.value = `You interacted with ${characterName}!`
}
</script>

<template>
  <main>
    <h1>* Characters</h1>

    <div class="characters">
      <CharacterCard name="Kris" :hp="90" @interact="handleInteraction" />

      <CharacterCard name="Susie" :hp="120" @interact="handleInteraction" />

      <CharacterCard name="Ralsei" :hp="70" @interact="handleInteraction" />
    </div>

    <p class="message">* {{ message }}</p>
  </main>
</template>

<style scoped>
main {
  max-width: 1000px;
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
  padding: 15px;
  border: 2px solid white;
}

@media (max-width: 700px) {
  .characters {
    grid-template-columns: 1fr;
  }
}
</style>
