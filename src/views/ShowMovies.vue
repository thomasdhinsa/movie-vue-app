<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log("Movies Show:", response.data);
      this.recipe = response.data;
    });
  },
  methods: {
    destroyRecipe: function () {
      if (confirm("Are you sure you to delete this?")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log("Success", response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>

<template>
  <div class="movies-show">
    <h2>{{ movie.title }}</h2>
    <img v-bind:src="movie.imageUrl" alt="" />
    <p>Title: {{ movie.title }}</p>
    <p>Year: {{ movie.year }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <p>Director: {{ movie.director }}</p>
    <p>English: {{ movie.english }}</p>
    <div v-if="movie.owner">
      <button>
        <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit</router-link>
      </button>
      |
      <button v-on:click="destroyMovie()">Delete</button>
    </div>
  </div>
</template>
