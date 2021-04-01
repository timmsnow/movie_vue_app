<template>
  <div class="movies-show">
    <div class="card" style="width: 18rem">
      <!-- <img src="..." class="card-img-top" alt="..."> -->
      <div class="card-body">
        <h2 class="card-title">{{ movie.title }}</h2>
        <p style="font-weight: bold" class="card-text">
          {{ movie.year }} • {{ movie.director }} • "{{ movie.genre[0] }}"
        </p>
        <p>{{ movie.plot }}</p>
        <router-link v-bind:to="`/movies/${movie.id}/edit`">Update That Movie</router-link>
        <br />
        <button v-on:click="destroyMovie(movie)">Delete Movie</button>
      </div>
    </div>

    <!-- 
    <div class="container">
      <h2>{{ movie.title }}</h2>
      <p style="font-weight: bold">{{ movie.year }} • {{ movie.director }} • "{{ movie.genre[0] }}"</p>
      <p>{{ movie.plot }}</p>
    </div>
    <router-link v-bind:to="`/movies/${movie.id}/edit`">Update That Movie</router-link>
    <br />
    <button v-on:click="destroyMovie(movie)">Delete Movie</button> -->
  </div>
</template>

<style>
.movies-show {
  display: flex;
  justify-content: center;
  padding-top: 5%;
  padding-bottom: 5%;
  background: linear-gradient(#fff, #ecc8fa);
}


button {
  margin-top: 5% !important;
  margin-bottom: 5%;
  background: rgb(2, 0, 36);
  background: purple;
  box-shadow: 1px 2px 5px black;
  color: white;
  text-shadow: 1px 1px 2px black;
}

h2 {
  font-family: "Exo 2", sans-serif;
  color: rgb(235, 5, 235);
  text-shadow: 1px 2px 4px silver, 1px 1px 1px black;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "It's MOVIE time",
      movie: {},
    };
  },
  created: function () {
    this.showMovies();
  },
  methods: {
    showMovies: function () {
      axios.get("api/movies/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.movie = response.data;
      });
    },
    destroyMovie: function (movie) {
      axios.delete("/api/movies/" + movie.id).then(() => {
        console.log("destroyed!");
        this.$router.push("/movies");
      });
    },
  },
};
</script>
