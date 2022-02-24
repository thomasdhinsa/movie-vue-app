<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
      errors: [],
    };
  },
  mounted: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log("Movie to edit:", response.data);
      this.movie = response.data;
    });
  },
  methods: {
    updateMovie: function () {
      axios
        .patch(`/movies/${this.movie.id}`, this.movie)
        .then((response) => {
          console.log("Updated Movie:", response.data);
          localStorage.setItem("flashMessage", "Movie successfully updated!");
          this.$router.push(`/movies/${this.movie.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovie()">
      <h1>Edit Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <p>Current movie: {{ movie }}</p>
      <p><img v-bind:src="movie.imageUrl" alt="" /></p>
      <div>
        <label>Title:</label>
        <input type="text" v-model="movie.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="movie.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="movie.plot" />
      </div>
      <div>
        <label>Director:</label>
        <input type="text" v-model="movie.director" />
      </div>
      <div>
        <label>Image Url:</label>
        <input type="text" v-model="movie.imageUrl" />
      </div>
      <div>
        <label>English?:</label>
        <input type="text" v-model="movie.english" />
      </div>
      <input type="submit" value="Update" />
    </form>
  </div>
</template>
;
