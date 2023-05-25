<template>
    <div>
      <ul>
        <li v-for="movie in movies" :key="movie.id">{{ movie.title }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['movies'],
  };
  </script>
  