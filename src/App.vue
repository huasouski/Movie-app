<template>
  <div class="app">
    <h1>Película más popular</h1>
    <SearchBar @search="searchMovies" />
    <div v-if="popularMovie">
      <h2>{{ popularMovie.title }}</h2>
      <p>{{ popularMovie.overview }}</p>
      <img :src="'https://image.tmdb.org/t/p/w500/' + popularMovie.poster_path" :alt="popularMovie.title" />
    </div>
    <div v-else>
      <p>Cargando...</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';

export default {
  components: {
    SearchBar,
  },
  data() {
    return {
      popularMovie: null,
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
            api_key: 'TU_CLAVE_DE_API',
          },
        })
        .then(response => {
          this.popularMovie = response.data.results[0];
        })
        .catch(error => {
          console.error(error);
        });
    },
    searchMovies(query) {
      axios
        .get('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: '0cf648c260a872eaeec076543d5ffe10',
            query: query,
          },
        })
        .then(response => {
          if (response.data.results.length > 0) {
            this.popularMovie = response.data.results[0];
          } else {
            this.popularMovie = null;
          }
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>












<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
