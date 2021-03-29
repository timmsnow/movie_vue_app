<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <div id="add_movie">
      <button v-on:click="createMovie()">Add a Movie to the List!</button>
      <div id="inp">
        <input type="text" placeholder="Movie Title" v-model="newMovieTitle" />
        <input type="text" placeholder="Year" v-model="newMovieYear" />
        <input type="text" placeholder="Director" v-model="newMovieDirector" />
        <input type="text" placeholder="Plot" v-model="newMoviePlot" />
      </div>
    </div>

    <div id="movieList" v-for="movie in movies" v-bind:key="movie.id">
      <h2 style="color: rgb(133, 133, 247)">{{ movie.title }}</h2>
      <button v-on:click="showMovie(movie)">See Movie Info</button>
    </div>

    <dialog id="movie-info">
      <form method="dialog">
        <h1>Update Movie Info</h1>
        <h2>
          Title:
          <input type="text" v-model="currentMovie.title" />
        </h2>
        <p>
          Year:
          <input type="text" v-model="currentMovie.year" />
        </p>
        <p>
          Director:
          <input type="text" v-model="currentMovie.director" />
        </p>
        <p>
          Plot:
          <textarea rows="5" type="text" v-model="currentMovie.plot" style="height: 100px" />
        </p>
        <button v-on:click="updateMovie(currentMovie)">Update that movie!</button>
        <button v-on:click="destroyMovie(currentMovie)">Delete ME</button>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style>
.home {
  padding-top: 5%;
  padding-bottom: 5%;
  background: linear-gradient(rgb(68, 68, 68), #fff);
}

#add_movie {
  display: inline-flex;
}

#add_movie button {
  margin-right: 5%;
  margin-top: 7%;
  margin-bottom: 7%;
  background: rgb(2, 0, 36);
  background: linear-gradient(
    90deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(154, 90, 228, 0.18333333333333335) 35%,
    rgba(0, 212, 255, 1) 100%
  );
  box-shadow: 1px 2px 5px black;
  color: white;
  text-shadow: 1px 1px 2px black;
}

#add_movie #inp {
  display: flex;
  flex-direction: column;
}

::placeholder {
  color: rgba(212, 146, 250, 0.699);
  font-size: 1em;
}

h1 {
  font-family: "Exo 2", sans-serif;
  color: rgb(235, 5, 235);
  text-shadow: 1px 2px 3px black;
}

#movieList {
  font-family: "Exo 2", sans-serif;
  text-shadow: 1px 2px 3px black;
}

#movieList p {
  text-shadow: 1px 1px 1px black;
  color: #ffffff;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "It's MOVIE time",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      currentMovie: {},
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
    createMovie: function () {
      console.log("Creating a recipe!");
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        director: this.newMovieDirector,
        genre: this.newMovieGenre,
      };
      axios
        .post("/api/movies", params)
        .then((response) => {
          console.log("sucessfully created movie!", response.data);
          this.movies.push(response.data);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
    showMovie: function(movie) {
      console.log(movie.id);
      this.currentMovie = movie;
      document.querySelector("#movie-info").showModal();
    },
    updateMovie: function (movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
      };
      axios.patch(`/api/movies/${movie.id}`, params).then((response) => {
        console.log("Updated!", response.data);
      });
    },
    destroyMovie: function (movie) {
      console.log(movie.id);
      axios.delete("/api/movies/" + movie.id).then((response) => {
        console.log("destroyed!", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>
