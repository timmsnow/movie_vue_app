<template>
  <div class="index">
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">It's all about the MOVIES</h1>
        <p class="lead">Welcome to the movie List... scroll down to see MOVIES</p>
        <p>or</p>
        <router-link to="/movies/new">Add a New Movie</router-link>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <div class="card" style="width: 18rem" id="movies-index" v-for="movie in movies" v-bind:key="movie.id">
          <!-- <img src="..." class="card-img-top" alt="..." /> -->
          <div class="card-body">
            <router-link style="text-decoration: none" v-bind:to="`movies/${movie.id}`">
              <h2 class="card-title">{{ movie.title }}</h2>
            </router-link>
            <p class="card-text">{{ movie.plot }}</p>
            <router-link v-bind:to="`/movies/${movie.id}`" class="btn btn-primary">Show Movie Info</router-link>
          </div>
        </div>
        <div class="col-sm"></div>
        <div class="col-sm"></div>
        <div class="col-sm"></div>
      </div>
    </div>

    <!-- <a href="#" class="btn btn-primary">See Movie Info</a> -->
    <!-- <button v-on:click="showMovies(movie)">See Movie Info</button> -->
    <!-- <div id="movies-index" v-for="movie in movies" v-bind:key="movie.id"> -->
    <!-- </div> -->
  </div>
</template>

<style>
.index {
  padding-top: 5%;
  padding-bottom: 5%;
  background: linear-gradient(#fff, #ecc8fa);
}

h1 {
  font-family: "Exo 2", sans-serif;
  color: rgb(235, 5, 235);
  text-shadow: 1px 2px 3px black;
}

.index h2 {
  color: #b502fa;
  text-shadow: 1px 2px 5px silver, 1px 1px 1px black;
}

.row {
  gap: 5%;
}

.card {
  margin-bottom: 2%;
  box-shadow: 1px 2px 5px silver, 1px 1px black;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
  },
};
</script>
