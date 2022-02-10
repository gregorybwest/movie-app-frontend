<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
      newMovieParams: {},
      currentMovie: {},
      editMovieParams: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      axios.post("/movies", this.newMovieParams).then((response) => {
        console.log("Success!", response.data);
        this.movies.push(response.data);
        this.newMovieParams = {};
      });
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      this.editMovieParams = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      axios.patch(`/movies/${movie.id}`, movie).then((response) => {
        console.log("Success!", response.data);
      });
    },
    destroyMovie: function (movie) {
      axios.delete(`/movies/${movie.id}`).then((response) => {
        console.log("Success!", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h3>New Movie</h3>
    <!-- <p>{{ newMovieParams }}</p> -->
    <div>
      Title:
      <input type="text" v-model="newMovieParams.title" />
      <br />
      Year:
      <input type="text" v-model="newMovieParams.year" />
      <br />
      Plot:
      <input type="text" v-model="newMovieParams.plot" />
      <br />
      English:
      <input type="text" v-model="newMovieParams.english" />
      <br />
      <button v-on:click="createMovie()">Create</button>
    </div>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>
        {{ movie.title }}
      </h2>
      <button v-on:click="showMovie(movie)">Movie Info</button>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info</h1>
        <p>
          Title:
          <input type="text" v-model="editMovieParams.title" />
        </p>
        <p>
          Year:
          <input type="text" v-model="editMovieParams.year" />
        </p>
        <p>
          Plot:
          <input type="text" v-model="editMovieParams.plot" />
        </p>
        <p>
          English:
          <input type="text" v-model="editMovieParams.english" />
        </p>
        <button v-on:click="updateMovie(currentMovie)">Update</button>
        <button v-on:click="destroyMovie(currentMovie)">Delete</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>
