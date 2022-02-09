<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "It's Working!",
    };
  },
  created: function () {},
  methods: {
    indexMovies: function () {
      console.log("do you see bananaman");
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>All Movies</h1>
    <button v-on:click="indexMovies()">Load Movies</button>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
    </div>
  </div>
</template>
<style></style>
