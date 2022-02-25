<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "It's Working!",
      movies: [],
      newMovieParams: {},
    };
  },
  mounted: function () {},
  methods: {
    createMovie: function () {
      axios.post("http://localhost:3000/movies", this.newMovieParams).then((response) => {
        console.log("Created!", response.data);
        this.movies.push(response.data);
        this.newMovieParams = {};
      });
    },
  },
};
</script>

<template>
  <form action=""></form>
  <div class="home">
    <h1>Create Movie</h1>
    <p>{{ newMovieParams }}</p>
    <div>
      <label for="Title">Title</label>
      <input type="text" v-model="newMovieParams.title" />
    </div>
    <div>
      <label for="Year">Year</label>
      <input type="integer" v-model="newMovieParams.year" />
    </div>
    <div>
      <label for="Plot">Plot</label>
      <input type="text" v-model="newMovieParams.plot" />
    </div>
    <div>
      <label for="Director">Director</label>
      <input type="text" v-model="newMovieParams.director" />
    </div>
    <div>
      <label for="English">English(True/False):</label>
      <input type="boolean" v-model="newMovieParams.english" />
    </div>
    <div>
      <label for="imageUrl">ImageUrl</label>
      <input type="text" v-model="newMovieParams.imageUrl" />
    </div>
    <button v-on:click="createMovie()">Create Movie</button>
  </div>
</template>
<style></style>
