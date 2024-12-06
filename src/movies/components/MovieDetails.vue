<template>
    <div class="details-container">
      <div class="row">
        <div class="col-md-4">
          <img
            :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
            :alt="movie.title"
            class="movie-poster"
          />
        </div>
        <div class="col-md-8">
          <h2>{{ movie.title }}</h2>
          <p><strong>Resumen:</strong> {{ movie.overview || 'No disponible.' }}</p>
          <p><strong>Calificación:</strong> ⭐ {{ movie.vote_average }}</p>
          <p><strong>Autores:</strong> {{ authors }}</p>
          <RouterLink class="btn btn-secondary mt-3" to="/movie">Volver a la lista</RouterLink>
        </div>
      </div>
    </div>
</template>
  
<script setup>
    import { ref, onMounted } from 'vue';
    import { useRoute } from 'vue-router';
    import axios from 'axios';

    const route = useRoute();
    const movie = ref({});
    const authors = ref('N/A');
    const api_key = 'ca2631092309ff919771ed949ab15677';

    const fetchMovieDetails = async () => {
    const movieId = route.params.id;
    const movieApiUrl = `https://api.themoviedb.org/3/movie/${movieId}?api_key=${api_key}&language=es-ES`;
    const creditsApiUrl = `https://api.themoviedb.org/3/movie/${movieId}/credits?api_key=${api_key}&language=es-ES`;

    try {
        // Fetch movie details
        const movieResponse = await axios.get(movieApiUrl);
        movie.value = movieResponse.data;

        // Fetch movie credits
        const creditsResponse = await axios.get(creditsApiUrl);
        authors.value =
        creditsResponse.data.crew
            ?.filter((crew) => crew.job === 'Director')
            .map((crew) => crew.name)
            .join(', ') || 'No disponible';
    } catch (error) {
        console.error('Error fetching movie details or credits:', error);
    }
    };

    onMounted(fetchMovieDetails);
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