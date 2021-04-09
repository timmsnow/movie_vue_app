<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="/">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <span v-if="ifLoggedIn()">
            <router-link to="/logout">
              <li class="nav-item">
                <a class="nav-link disabled" href="" tabindex="-1" aria-disabled="true">Log Out</a>
              </li>
            </router-link>
          </span>
          <span v-if="!ifLoggedIn()">
            <router-link to="/signup">
              <li class="nav-item active">
                <a class="nav-link" href="">Sign Up</a>
              </li>
            </router-link>
          </span>
          <span v-if="!ifLoggedIn()">
            <router-link to="/login">
              <li class="nav-item">
                <a class="nav-link" href="">Log In</a>
              </li>
            </router-link>
          </span>
          <router-link to="/movies">
            <li class="nav-item">
              <a class="nav-link" href="">
                All Movies
                <span class="sr-only">(current)</span>
              </a>
            </li>
          </router-link>
          <router-link to="/movies/new">
            <li class="nav-item">
              <a class="nav-link" href="">
                Add a New Movie
                <span class="sr-only">(current)</span>
              </a>
            </li>
          </router-link>

          <!-- <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >
              Dropdown
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a class="dropdown-item" href="#">Action</a>
              <a class="dropdown-item" href="#">Another action</a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#">Something else here</a>
            </div>
          </li> -->
        </ul>
        <!-- <form class="form-inline my-2 my-lg-0">
          <span>
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button></span>
        </form> -->
      </div>
    </nav>

    <!-- <div id="nav">
      <router-link to="/">Home</router-link>
      |
      <router-link to="/about">About</router-link>
      |
      <router-link to="/login">Log In</router-link>
      |
      <router-link to="/logout">Log Out</router-link>
      |
      <router-link to="/movies">All Movies</router-link>
    </div> -->
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

.lead {
  margin-top: 5%;
}

.btn-primary {
  background-color: #b414f3 !important;
}
</style>

<script>
export default {
  methods: {
    ifLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
    // getUserId: function () {
    //   return localStorage.getItem("user_id");
    // },
  },
};
</script>
