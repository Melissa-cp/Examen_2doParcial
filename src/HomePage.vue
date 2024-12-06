<template>
    <div class="home">
      <!-- Sección de bienvenida -->
      <div class="hero-section">
        <h1 class="hero-title">¡Bienvenido a Películas y Series!</h1>
        <p class="hero-subtitle">Descubre y explora las mejores películas y series de televisión.</p>
       
      </div>
  
      <!-- Sección destacada -->
      <div class="highlight-section">
        <div class="highlight-item movies">
          <div class="highlight-overlay">
            <h2>Películas</h2>
            <p>Explora las películas más populares y actuales en cartelera.</p>
            <RouterLink to="/movie" class="btn btn-warning">Explorar Películas</RouterLink>
          </div>
        </div>
        <div class="highlight-item series">
          <div class="highlight-overlay">
            <h2>Series de TV</h2>
            <p>Descubre las mejores series de televisión y tendencias actuales.</p>
            <RouterLink to="/tv" class="btn btn-warning">Explorar Series</RouterLink>
          </div>
        </div>
      </div>
    </div>
</template>
  
<script setup>
  import { RouterLink } from 'vue-router';
</script>
  
<style>
  /* Estilos generales */
  body {
    font-family: 'Arial', sans-serif;
    margin: 0;
    background-color: #123c63;
    color: white;
  }
  
  /* Estilo para la sección de bienvenida */
  .hero-section {
    text-align: center;
    padding: 50px 20px;
    background: linear-gradient(45deg, #154c79, #1e6b9d);
    color: white;
  }
  
  .hero-title {
    font-size: 2.5rem;
    margin-bottom: 10px;
  }
  
  .hero-subtitle {
    font-size: 1.2rem;
    margin-bottom: 30px;
  }
  
  .hero-buttons .btn {
    margin: 10px;
    padding: 10px 20px;
    border-radius: 5px;
    transition: background-color 0.3s ease;
  }
  
  .hero-buttons .btn-primary {
    background-color: #ff9800;
    border: none;
    color: white;
  }
  
  .hero-buttons .btn-secondary {
    background-color: #00bcd4;
    border: none;
    color: white;
  }
  
  .hero-buttons .btn:hover {
    background-color: #ff5722;
    color: white;
  }
  
  /* Estilo para la sección destacada */
  .highlight-section {
    display: flex;
    flex-wrap: wrap;
    margin-top: 50px;
  }
  
  .highlight-item {
    position: relative;
    flex: 1 1 calc(50% - 20px);
    margin: 10px;
    height: 300px;
    border-radius: 10px;
    overflow: hidden;
    background-size: cover;
    background-position: center;
  }
  
  .highlight-item.movies {
    background-image: url('https://image.tmdb.org/t/p/original/zM9RGbJBZ3UNpFOabcRqh0iVAYP.jpg'); /* Fondo ejemplo de películas */
  }
  
  .highlight-item.series {
    background-image: url('https://image.tmdb.org/t/p/original/vWcHsHmjRp9vZK6vCpjrSuJFeXg.jpg'); /* Fondo ejemplo de series */
  }
  
  .highlight-overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.6);
    color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 20px;
    text-align: center;
  }
  
  .highlight-overlay h2 {
    font-size: 2rem;
    margin-bottom: 10px;
  }
  
  .highlight-overlay p {
    font-size: 1.1rem;
    margin-bottom: 20px;
  }
  
  .highlight-overlay .btn {
    padding: 10px 20px;
    border-radius: 5px;
    color: white;
    background-color: #ff9800;
    border: none;
    transition: background-color 0.3s ease;
  }
  
  .highlight-overlay .btn:hover {
    background-color: #ff5722;
  }
  </style>