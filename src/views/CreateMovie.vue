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
  created: function () {},
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
  </div>
</template>
<style></style>
