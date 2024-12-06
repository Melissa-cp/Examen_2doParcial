<template>
    <div class="details-container">
      <div class="row">
        <div class="col-md-4">
          <img
            :src="`https://image.tmdb.org/t/p/w500${series.poster_path}`"
            :alt="series.name"
            class="movie-poster"
          />
        </div>
        <div class="col-md-8">
          <h2>{{ series.name }}</h2>
          <p><strong>Resumen:</strong> {{ series.overview }}</p>
          <p><strong>Calificación:</strong> ⭐ {{ series.vote_average || 'N/A' }}</p>
          <p><strong>Creador:</strong> {{ creators }}</p>
          <RouterLink class="btn btn-secondary mt-3" to="/tv">Volver a la lista</RouterLink>
        </div>
      </div>
    </div>
</template>
  
<script setup>
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  import axios from 'axios';
  
  const route = useRoute();
  const series = ref({});
  const creators = ref('N/A');
  const api_key = 'ca2631092309ff919771ed949ab15677';
  
  const fetchSeriesDetails = async () => {
    const seriesId = route.params.id;
    const seriesApiUrl = `https://api.themoviedb.org/3/tv/${seriesId}?api_key=${api_key}&language=es-ES`;
    const creditsApiUrl = `https://api.themoviedb.org/3/movie/${seriesId}/credits?api_key=${api_key}&language=es-ES`;
    try {
      // Fetch series details
      const seriesResponse = await axios.get(seriesApiUrl);
      //console.log('Detalles de la serie:', seriesResponse.data);
      series.value = seriesResponse.data;
        //creditos
        const creditsResponse=await axios.get(creditsApiUrl);
        creators.value=creditsResponse.data.crew ?.filter((crew)=> crew.job=='Creador').map((crew)=>crew.name).join(', '|| 'No disponible');
      // Extraer creadores si existen
      if (seriesResponse.data.created_by && seriesResponse.data.created_by.length > 0) {
        creators.value = seriesResponse.data.created_by.map((creator) => creator.name).join(', ');
      } else {
        creators.value = 'No disponible.';
      }
    } catch (error) {
      console.error('Error al obtener los detalles de la serie:', error);
    }
  };
  
  onMounted(fetchSeriesDetails);
</script>
  
<style>
    .details-container {
      background-color: #123c63;
      color: white;
      padding: 20px;
    }
  
    .movie-poster {
      width: 100%;
      border-radius: 10px;
    }
  
    h2 {
      color: #ffcc00;
    }
  
    .btn {
      color: white;
      background-color: #154c79;
      border: none;
    }
  
    .btn:hover {
      background-color: #1e6b9d;
    }
</style>