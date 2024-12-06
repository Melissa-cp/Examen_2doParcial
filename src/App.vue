<template>
  <div class="app">
    <nav class="menu">
      <RouterLink to="/" class="link">Inicio</RouterLink>
      <RouterLink to="/movie" class="link">Películas</RouterLink>
      <RouterLink to="/tv" class="link">Series de TV</RouterLink>
      
    </nav>
    <div class="container">
      <RouterView />
    </div>
  </div>
</template>

<script setup>
  import { RouterLink, RouterView } from 'vue-router';
</script>

<style>
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  background-color: #123c63;
  color: white;
}

.menu {
  display: flex;
  justify-content: center;
  padding: 10px;
  background-color: #154c79;
}

.link {
  margin: 0 15px;
  text-decoration: none;
  color: white;
}

.link:hover {
  background-color: #1e6b9d;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}

.container {
  padding: 20px;
}
</style>
