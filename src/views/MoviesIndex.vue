<template>
  <div class="index">
    <h1>{{ message }}</h1>
    <router-link to="/movies/new">Add a New Movie</router-link>

    <div id="movies-index" v-for="movie in movies" v-bind:key="movie.id">
      <router-link style="text-decoration: none;" v-bind:to="`movies/${movie.id}`">
        <h2>{{ movie.title }}</h2>
      </router-link>
      <!-- <button v-on:click="showMovie(movie)">See Movie Info</button> -->
    </div>
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

</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "It's MOVIE time",
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies/").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
  },
};
</script>
