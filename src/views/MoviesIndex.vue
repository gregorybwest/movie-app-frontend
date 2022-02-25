<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
      titleFilter: "",
    };
  },
  created: function () {
    this.moviesIndex();
  },
  methods: {
    moviesIndex: function () {
      axios.get("/movies").then((response) => {
        console.log("movie index:", response.data);
        this.movies = response.data;
      });
    },
  },
  computed: {
    filteredMovies() {
      return this.movies.filter((movie) => {
        return movie.title.toLowerCase().includes(this.titleFilter.toLowerCase());
      });
    },
  },
};
</script>

<template>
  <div class="movies-index">
    <div class="container">
      <div class="row row-cols-2 row-cols-md-3 g-4">
        <div class="col" v-for="movie in movies" v-bind:key="movie.id">
          <div class="card">
            <img src="https://www.placecage.com/300/200" class="card-img-top" alt="..." />
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }}</h5>
              <p class="card-text">
                {{ movie.plot }}
              </p>
              <router-link
                href="#"
                class="btn btn-primary btn-lg enabeled"
                tabindex="-1"
                role="button"
                aria-disabled="true"
                v-bind:to="`/movies/${movie.id}`"
              >
                More Info
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
    Search by Title:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <h1>All Movies:</h1>
    <br />
    <transition-group
      appear
      enter-active-class="animate__animated animate__fadeIn"
      leave-active-class="animate__animated animate__fadeOut"
    >
      <div v-for="movie in filteredMovies" v-bind:key="movie.id">
        <h2>{{ movie.title }}</h2>
        <h3>{{ movie.year }}</h3>
        <router-link v-bind:to="`/movies/${movie.id}`">More Info</router-link>
      </div>
    </transition-group>
  </div>
</template>

<style></style>
