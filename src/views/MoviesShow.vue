<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log("movies show", response.data);
      this.movie = response.data;
    });
  },
  methods: {
    moviesDestroy: function () {
      axios.delete("/movies/" + this.movie.id).then((response) => {
        console.log("Movie destroyed", response.data);
        this.$router.push("/movies");
      });
    },
  },
};
</script>

<!-- <template>
  <div class="movies-show">
    <h1>{{ movie.plot }}</h1>
    <router-link to="/movies">Back to all movies</router-link>
  </div>
</template> -->

<template>
  <div class="movies-show">
    <h2>{{ movie.plot }}</h2>
    <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit movie</router-link>
    <br />
    <router-link to="/movies">Back to all movies</router-link>
    <br />
    <button v-on:click="moviesDestroy()">Delete</button>
  </div>
</template>

<style></style>
