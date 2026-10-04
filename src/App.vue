<script setup>
import Header from './components/Header.vue'
</script>

<template>
  <Header />

  <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/characters">Characters</RouterLink>
    <RouterLink to="/about">About</RouterLink>
  </nav>

  <RouterView />
</template>

<style scoped>
nav {
  display: flex;
  justify-content: center;
  gap: 30px;
  padding: 20px;
  background-color: black;
  border-bottom: 2px solid white;
}

nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

nav a:hover {
  color: #ffcc00;
}

nav a.router-link-active {
  color: #ffcc00;
}
</style>
