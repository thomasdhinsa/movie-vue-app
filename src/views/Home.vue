<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "It's Working!",
      newMovieParams: {},
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
      axios.post("http://localhost:3000/movies", this.newMovieParams).then((response) => {
        console.log("Created!", response.data);
        this.movies.push(response.data);
        this.newMovieParams = {};
      });
    },
    movieShow: function (movie) {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(movie.title);
        this.movies = response.data;
      });
    },
    movieUpdate: function () {
      var params = {};
      axios.patch("http://localhost:3000/movies", params).then((response) => {
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
    <p>{{ newMovieParams }}</p>
    <div>
      Title:
      <input type="text" v-model="newMovieParams.title" />
    </div>
    <div>
      Year:
      <input type="integer" v-model="newMovieParams.year" />
    </div>
    <div>
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
    </div>
    <div>
      Director:
      <input type="text" v-model="newMovieParams.director" />
    </div>
    <div>
      English(True/False):
      <input type="boolean" v-model="newMovieParams.english" />
    </div>
    <div>
      Imageurl:
      <input type="text" v-model="newMovieParams.imageUrl" />
    </div>
    <button v-on:click="createMovie()">Create Movie</button>
    <h1>All Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h1>Title: {{ movie.title }}</h1>
      <img v-bind:src="movie.imageUrl" alt="" />
    </div>
    <button v-on:click="indexMovies()">Load Movie</button>
    <h1>View Movie</h1>
    <button v-on:click="movieShow(movie)">Load Movie</button>
    <h1>Update Movie</h1>
    <button v-on:click="movieUpdate()">Update Movie</button>
    <h1>Delete Movie</h1>
    <button v-on:click="movieDelete()">Delete Movie</button>
  </div>
</template>
<style></style>
