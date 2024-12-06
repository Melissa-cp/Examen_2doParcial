<template>
    <div>
      <Lodging v-if="isLoading" />
      <div v-else>
        <h3 class="display-6 text-warning text-center">Películas en Cartelera</h3>
        <div class="row">
          <div class="col-md-4 mb-4" v-for="movie in nowplaying" :key="movie.id">
            <RouterLink :to="`/movie/${movie.id}`" class="card-link">
              <div class="card h-100">
                <img
                  :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
                  :alt="movie.title"
                  class="card-img-top"
                />
                <div class="card-body text-center">
                  <h5 class="card-title">{{ movie.title }}</h5>
                </div>
              </div>
            </RouterLink>
          </div>
        </div>
      </div>
    </div>
</template>
  
<script setup>
  import { ref } from 'vue';
  import { RouterLink } from 'vue-router';
  import Lodging from './components/Lodging.vue';
  
  const api_key = 'ca2631092309ff919771ed949ab15677';
  const base_url = `https://api.themoviedb.org/3/movie/now_playing?api_key=${api_key}`;
  
  const isLoading = ref(true);
  const nowplaying = ref([]);
  
  const getNowPlayingMovies = async () => {
    isLoading.value = true;
    const resp = await fetch(base_url);
    const data = await resp.json();
    nowplaying.value = data.results.map((movie) => ({
      id: movie.id,
      title: movie.title,
      overview: movie.overview,
      poster_path: movie.poster_path,
    }));
    isLoading.value = false;
  };
  
    getNowPlayingMovies();
</script>
  
<style>
    .row {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
        justify-content: center;
    }
  
    .card {
        background-color: #154c79;
        color: white;
        border: none;
        transition: transform 0.2s ease;
    }
    
    .card:hover {
        transform: scale(1.05);
    }
    
    .card-img-top {
        border-radius: 5px;
    }
  
    .card-title {
        font-size: 1.1em;
        margin: 10px 0;
    }
  
    .card-link {
        text-decoration: none;
        color: inherit;
    }
</style>