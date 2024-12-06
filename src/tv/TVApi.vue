<template>
    <div>
      <Lodging v-if="isLoading" />
      <div v-else>
        <h3 class="display-6 text-warning text-center">Series Populares</h3>
        <div class="row">
          <div class="col-md-4 mb-4" v-for="tv in popularSeries" :key="tv.id">
            <RouterLink :to="`/tv/${tv.id}`" class="card-link">
              <div class="card h-100">
                <img
                  :src="`https://image.tmdb.org/t/p/w500${tv.poster_path}`"
                  :alt="tv.name"
                  class="card-img-top"
                />
                <div class="card-body text-center">
                  <h5 class="card-title">{{ tv.name }}</h5>
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
  import axios from 'axios';
  //import TVLodging from './components/TVLodging.vue'; 
  
  const api_key = 'ca2631092309ff919771ed949ab15677';
  const base_url = `https://api.themoviedb.org/3/tv/popular?api_key=${api_key}&language=es-ES`;
  
  const isLoading = ref(true);
  const popularSeries = ref([]);
  
  const fetchPopularSeries = async () => {
    isLoading.value = true;
    try {
      const resp = await axios.get(base_url);
      console.log(resp.data); // Verifica la respuesta de la API

      // Mapear los datos recibidos y asignarlos a la variable popularSeries
      popularSeries.value = resp.data.results.map((tv) => ({
        id: tv.id,
        name: tv.name,
        overview: tv.overview,
        poster_path: tv.poster_path,
      }));
    } catch (error) {
      console.error('Error fetching popular series:', error);
    }
    isLoading.value = false;
  };
  
  fetchPopularSeries();
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