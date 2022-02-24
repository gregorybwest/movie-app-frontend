<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newMovieParams: { plot: "" },
      errors: [],
      sadStatus: "",
    };
  },
  created: function () {},
  methods: {
    moviesCreate: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log("New Movie:", response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("movies create error", error.response);
          this.sadStatus = error.response.status;
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="movies-new">
    <form v-on:submit.prevent="moviesCreate()">
      <h1>New Movie</h1>
      <img v-if="sadStatus" v-bind:src="`https://http.cat/${sadStatus}`" alt="" />
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="newMovieParams.title" />
      <br />
      Year:
      <input type="text" v-model="newMovieParams.year" />
      <br />
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
      <br />
      <small>{{ 100 - newMovieParams.plot.length }} characters remaining</small>
      <br />
      English:
      <input type="text" v-model="newMovieParams.english" />
      <br />
      <input type="submit" value="Create" />
      <p>{{ newMovieParams }}</p>
    </form>
  </div>
</template>

<style>
input[type="text"] {
  -webkit-appearance: none;
  appearance: none;
}
</style>
