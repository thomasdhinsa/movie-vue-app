<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "It's Working!",
      movies: [],
      newMovieParams: {},
      currentMovie: {},
      editMovieParams: {},
    };
  },
  mounted: function () {},
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
      console.log(movie);
      this.currentMovie = movie;
      this.editMovieParams = movie;
      document.querySelector("movie-details").showModal();
    },
    movieUpdate: function (movie) {
      axios.patch(`http://localhost:3000/movies/${movie.id}`, movie).then((response) => {
        console.log("Updated", response.data);
      });
    },
    movieDelete: function (movie) {
      axios.delete(`http://localhost:3000/movies/${movie.id}`, movie).then((response) => {
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
      <h1>Title {{ movie.title }}</h1>
      <img v-bind:src="movie.imageUrl" alt="" />
      <button v-on:click="movieShow(movie)">More Info</button>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info</h1>
        <p>Title: {{ currentMovie.title }}</p>
        <p>Year: {{ currentMovie.year }}</p>
        <p>Plot: {{ currentMovie.plot }}</p>
        <p>Director: {{ currentMovie.director }}</p>
        <p>English: {{ currentMovie.english }}</p>
        <img src="currentMovie.imageUrl" alt="" />
        <h2>Edit Movie</h2>
        <p>
          Title:
          <input type="text" v-model="editMovieParams.title" />
        </p>
        <p>
          Year:
          <input type="integer" v-model="editMovieParams.year" />
        </p>
        <p>
          Plot:
          <input type="text" v-model="editMovieParams.plot" />
        </p>
        <p>
          Director:
          <input type="text" v-model="editMovieParams.director" />
        </p>
        <p>
          English:
          <input type="boolean" v-model="editMovieParams.english" />
        </p>
        <p>
          Image Url:
          <input type="text" v-model="editMovieParams.imageUrl" />
        </p>
        <h1>Update Movie</h1>
        <button v-on:click="movieUpdate(currentMovie)">Update Movie</button>
        <h1>Delete Movie</h1>
        <button v-on:click="movieDelete(currentMovie)">Delete Movie</button>
        <button>Close</button>
      </form>
    </dialog>
    <button v-on:click="indexMovies()">Load Movies</button>
  </div>
</template>
<style></style>
