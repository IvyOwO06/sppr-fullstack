<script setup>
import { ref } from 'vue'

function loadFavourites() {
  try {
    return JSON.parse(localStorage.getItem('favourites')) || []
  } catch {
    return []
  }
}

const favourites = ref(loadFavourites())

const name = ref('')
const note = ref('')
const editingId = ref(null)
const feedback = ref('')
const feedbackType = ref('success')

function saveToStorage() {
  localStorage.setItem('favourites', JSON.stringify(favourites.value))
}

function saveFavourite() {
  feedback.value = ''

  if (!name.value.trim() || !note.value.trimEnd()) {
    feedback.value = 'Please fill in both the character name and note.'
    feedbackType.value = 'error'
    return
  }

  if (editingId.value !== null) {
    const favourite = favourites.value.find((item) => item.id === editingId.value)

    if (favourite) {
      favourite.name = name.value.trim()
      ;((favourite.note = note), value.trim())
    }

    feedback.value = 'Favourite updated successfully.'
  } else {
    favourites.value.push({
      id: Date.now(),
      name: name.value.trim(),
      note: note.value.trim(),
    })

    feedback.value = 'Favourite added successfully.'
  }

  saveToStorage()
  resetForm()
}

function editFavourite(favourite) {
  name.value = favourite.name
  note.value = favourite.note
  editingId.value = favourite.id
  feedback.value = ''
}

function deleteFavourite(id) {
  const updatedFavourites = favourites.value.filter((favourite) => favourite.id !== id)

  favourites.value = updatedFavourites

  localStorage.setItem('favourites', JSON.stringify(updatedFavourites))

  if (editingId.value === id) {
    resetForm()
  }

  feedbackType.value = 'success'
  feedback.value = 'Favourite deleted successfully.'
}

function resetForm() {
  name.value = ''
  note.value = ''
  editingId.value = null
}
</script>

<template>
  <main class="favourites-page">
    <h1>My Favourite Characters</h1>

    <form @submit.prevent="saveFavourite">
      <div class="form-group">
        <label for="character-name">Character name</label>
        <input
          type="text"
          v-model="name"
          id="character-name"
          maxlength="100"
          placeholder="Enter a character name"
          required
        />
      </div>

      <div class="form-group">
        <label for="character-note">Personal note</label>
        <textarea
          id="character-note"
          v-model="note"
          maxlength="500"
          placeholder="Why is this character a favourite"
          required
        ></textarea>
      </div>

      <button type="submit">
        {{ editingId !== null ? 'Save changes' : 'Add favourite' }}
      </button>

      <button v-if="editingId !== null" type="button" class="cancel-button" @click="resetForm">
        Cancel
      </button>
    </form>

    <p v-if="feedback" class="feedback" :class="feedbackType" role="status">
      {{ feedback }}
    </p>

    <section class="favourites-list">
      <h2>Saved favourites {{ favourites.length }}</h2>

      <p v-if="favourites.length === 0">You haven't added any favourites yet.</p>

      <article v-for="favourite in favourites" :key="favourite.id" class="favourite-card">
        <h3>{{ favourite.name }}</h3>
        <p>{{ favourite.note }}</p>

        <div class="actions">
          <button type="button" @click="editFavourite(favourite)">Edit</button>

          <button type="button" class="delete-button" @click="deleteFavourite(favourite.id)">
            Delete
          </button>
        </div>
      </article>
    </section>
  </main>
</template>

<style scoped>
.favourites-page {
  max-width: 800px;
  margin: 0 auto;
  padding: 40px 20px;
}

h1,
h2 {
  text-align: center;
}

form {
  padding: 25px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f8f8f8;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 20px;
}

input,
textarea {
  width: 100%;
  box-sizing: border-box;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font: inherit;
}

textarea {
  min-height: 100px;
  resize: vertical;
}

button {
  padding: 10px 16px;
  border: none;
  border-radius: 5px;
  background-color: #333;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #555;
}

.cancel-button {
  margin-left: 10px;
  background-color: #666;
}

.favourites-list {
  margin-top: 35px;
}

.favourite-card {
  margin-top: 15px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-sizing: border-box;
  max-width: 100%;
  min-width: 0;
  overflow-wrap: anywhere;
}

.favourite-card h3,
.favourite-card p {
  max-width: 100%;
  overflow-wrap: anywhere;
  word-break: normal;
  white-space: normal;
}

.favourite-card .actions {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.delete-button {
  background-color: #c62828;
}

.delete-button:hover {
  background-color: #a51f1f;
}

.feedback {
  margin-top: 20px;
  padding: 12px;
  border-radius: 5px;
}

.success {
  color: #176b2c;
  background-color: #e5f5e9;
}

.error {
  color: #b71c1c;
  background-color: #fde8e8;
}
</style>
