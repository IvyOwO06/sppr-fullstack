<script setup>
import Header from './components/Header.vue'
import CounterCard from './components/CounterCard.vue'
import CharacterCard from './components/CharacterCard.vue'
import { ref } from 'vue'

const message = ref('Choose a character to interact with!')

function handleInteraction(characterName) {
  message.value = `You interacted with ${characterName}!`
}
</script>

<template>
  <Header />

  <main>
    <CounterCard />

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
  margin: 40px auto;
  padding: 0 20px;
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
  background-color: black;
  color: white;
  text-align: center;
}

@media (max-width: 700px) {
  .characters {
    grid-template-columns: 1fr;
  }
}
</style>
