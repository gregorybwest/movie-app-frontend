<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
      editMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log(response.data);
      this.movie = response.data;
      this.editMovieParams = this.movie;
    });
  },
  methods: {
    moviesUpdate: function () {
      axios
        .patch("/movies/" + this.movie.id, this.editMovieParams)
        .then((response) => {
          console.log(response);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("photos update error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="movies-edit">
    <h1>Edit Movie</h1>
    <form v-on:submit.prevent="moviesUpdate(movie)">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="editMovieParams.title" />
      Year:
      <input type="text" v-model="editMovieParams.year" />
      Plot:
      <input type="text" v-model="editMovieParams.plot" />
      English:
      <input type="text" v-model="editMovieParams.english" />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<style></style>
