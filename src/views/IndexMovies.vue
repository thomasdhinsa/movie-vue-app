<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "It's Working!",
      movies: [],
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
      <h1>Title {{ movie.title }}</h1>
      <img v-bind:src="movie.imageUrl" alt="" />
    </div>
  </div>
</template>
<style></style>
