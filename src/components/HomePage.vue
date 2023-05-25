<template>
    <div>
      <h1>Película más popular</h1>
      <div v-if="movie">
        <h2>{{ movie.title }}</h2>
        <p>{{ movie.overview }}</p>
        <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" />
      </div>
      <div v-else>
        <p>Cargando...</p>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        movie: null,
      };
    },
    created() {
      this.fetchPopularMovie();
    },
    methods: {
      fetchPopularMovie() {
        axios
          .get('https://api.themoviedb.org/3/movie/popular', {
            params: {
              api_key: '0cf648c260a872eaeec076543d5ffe10',
            },
          })
          .then(response => {
            this.movie = response.data.results[0];
          })
          .catch(error => {
            console.error(error);
          });
      },
    },
  };
  </script>
  
  <style scoped>
  
  </style>
  