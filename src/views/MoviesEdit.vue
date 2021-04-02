<template>
  <div class="movies-edit">
    <div class="container">
      <h1>UPDATE MOVIE</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>

      <div class="row justify-content-md-center">
        <form v-on:submit.prevent="updateMovie(movie)">
          <div class="col-sm">
            <div class="form-group">
              <label>Title:</label>
              <input type="text" class="form-control" v-model="movie.title" />
            </div>
          </div>
          <div class="form-group">
            <label>Year:</label>
            <input type="text" class="form-control" v-model="movie.year" />
          </div>
          <div class="form-group">
            <label>Director:</label>
            <input type="text" class="form-control" v-model="movie.director" />
          </div>
          <div class="form-group">
            <label>Plot:</label>
            <input type="text" class="form-control" v-model="movie.plot" />
          </div>
          <input type="submit" class="btn btn-primary" value="Submit" />
        </form>
      </div>
    </div>
  </div>
</template>

<style>
.movies-edit {
  padding-top: 5%;
  padding-bottom: 5%;
  background: linear-gradient(#fff, #ecc8fa);
}

.btn-primary {
  margin-top: 5%;
  margin-bottom: 5%;
  background: rgb(2, 0, 36);
  background: purple;
  box-shadow: 1px 2px 5px black;
  color: white;
  text-shadow: 1px 1px 2px black;
}

h1 {
  font-family: "Exo 2", sans-serif;
  color: rgb(235, 5, 235);
  text-shadow: 1px 2px 3px black;
  margin-bottom: 8%;
}

.form-control {
  margin-bottom: 1%;
  margin-left: 1%;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "It's MOVIE time",
      errors: [],
      movie: {},
    };
  },
  created: function () {
    axios.get("/api/movies/" + this.$route.params.id).then((response) => {
      console.log(response.data);
      this.recipe = response.data;
    });
  },
  methods: {
    updateMovie: function (movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
      };
      axios
        .patch("/api/movies/" + this.$route.params.id, params)
        .then(() => {
          this.$router.push("/movies/");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
