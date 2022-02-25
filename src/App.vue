<script>
export default {
  data: function () {
    return {
      isLoggedIn: !!localStorage.jwt,
      flashMessage: null,
    };
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
      this.flashMessage = localStorage.flashMessage;
      localStorage.removeItem("flashMessage");
    },
  },
  methods: {},
};
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">The Movies App!</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <router-link class="nav-link active" to="/" aria-current="page" href="#">Home</router-link>
          <router-link class="nav-link" v-if="!isLoggedIn" to="/signup" href="#">Signup</router-link>
          <router-link class="nav-link" v-if="!isLoggedIn" to="/login" href="#">Login</router-link>
          <router-link class="nav-link" v-if="isLoggedIn" to="/logout" href="#">Logout</router-link>
          <router-link class="nav-link" to="/movies" href="#">All Movies</router-link>
          <router-link class="nav-link" v-if="isLoggedIn" to="/movies/new" href="#">Create Movie</router-link>
        </div>
      </div>
    </div>
  </nav>
  <router-view />
  <!-- <div id="nav">
    <router-link to="/">Home</router-link>
    |
    <router-link v-if="!isLoggedIn" to="/signup">Signup</router-link>
    |
    <router-link v-if="!isLoggedIn" to="/login">Login</router-link>
    |
    <router-link v-if="isLoggedIn" to="/logout">Logout</router-link>
    |
    <router-link to="/movies">All Movies</router-link>
    |
    <router-link to="/movies/new">Create Movie</router-link>
  </div> -->
  <!-- <router-view /> -->
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
