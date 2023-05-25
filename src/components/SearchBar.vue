<template>
    <div>
      <input type="text" v-model="query" placeholder="Buscar películas...">
      <button @click="searchMovies">Buscar</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        query: '',
      };
    },
    methods: {
      searchMovies() {
        this.$emit('search', this.query);
      },
    },
  };
  </script>
  
 