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
    createMovie: function () {
      var params = {
        title: "Matilda",
        year: 1996,
        plot: "The film centers on the titular child prodigy, Matilda Wormwood, who develops psychokinetic abilities and uses them to deal with her disreputable family; and Agatha Trunchbull, the ruthless, oppressive, and tyrannical principal of Crunchem Hall Elementary School.",
        director: "Danny DeVito",
        english: true,
      };
      axios.post("http://localhost:3000/movies", params).then((response) => {
        console.log("Created!", response.data);
      });
    },
    movieInfo: function () {
      axios.get("http://localhost:3000/movies/3").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    movieUpdate: function () {
      var params = {
        title: "stuff",
        year: 1996,
        plot: "stuff in more stuff checking update status",
        director: "stuff",
        english: true,
      };
      axios.patch("http://localhost:3000/movies/13", params).then((response) => {
        console.log("Updated", response.data);
      });
    },
    movieDelete: function () {
      axios.delete("http://localhost:3000/movies/10").then((response) => {
        console.log("Deleted", response.data);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>Create Movie</h1>
    <button v-on:click="createMovie()">Create Movie</button>
    <h1>All Movies</h1>
    <button v-on:click="indexMovies()">Load Movies</button>
    <h1>View Movie</h1>
    <button v-on:click="movieInfo()">Load Movie 3</button>
    <h1>Update Movie</h1>
    <button v-on:click="movieUpdate()">Update Movie</button>
    <h1>Delete Movie</h1>
    <button v-on:click="movieDelete()">Delete Movie</button>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
    </div>
  </div>
</template>
<style></style>
