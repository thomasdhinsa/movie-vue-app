<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "It's Working!",
      movies: [],
    };
  },
  mounted: function () {
    axios.get("/movies").then((response) => {
      console.log("Movies Index:", response.data);
      this.movies = response.data;
    });
  },
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
  <div class="movies-index">
    <div class="container">
      <transition-group
        appear
        enter-active-class="animate__animated animate__backInLeft"
        leave-active-class="animate__animated animate__backInRight"
      >
        <div class="col" v-for="movie in movies" v-bind:key="movie.id">
          <div class="card">
            <img v-bind:src="movie.image" alt="" />
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }}</h5>
              <p class="card-text">{{ movie.description }}</p>
              <a href="#" class="btn btn-primary">Go somewhere</a>
            </div>
          </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>
<style></style>
