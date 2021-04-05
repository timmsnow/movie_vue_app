<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <div class="movies-new">
      <form v-on:submit.prevent="createMovie()">
        <h1>New Movie</h1>
        <ul>
          <li class="text-danger" v-for="error in errors" v-bind:key="error">
            {{ error }}
          </li>
        </ul>
        <div class="form-group">
          <label>Title:</label>
          <input type="text" class="form-control" v-model="title" />
        </div>
        <div class="form-group">
          <label>Year:</label>
          <input type="text" class="form-control" v-model="year" />
        </div>
        <div class="form-group">
          <label>Director:</label>
          <input type="text" class="form-control" v-model="director" />
        </div>
        <div class="form-group">
          <label>Plot:</label>
          <input type="text" class="form-control" v-model="plot" />
        <small v-if="plot.length > 100" class="text-danger">That's too many words! Shut up already!</small>
        </div>
        <input type="submit" class="btn btn-primary" value="Submit" />
      </form>
    </div>
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

.text-danger {
  font-weight: bold;
}
</style>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "It's MOVIE TIME",
      title: "",
      year: "",
      plot: "",
      director: "",
      errors: {},
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      console.log("Creating a movie!");
      var params = {
        title: this.title,
        year: this.year,
        director: this.director,
        plot: this.plot,
      };
      axios
        .post("/api/movies", params)
        .then((response) => {
          console.log("sucessfully created movie!", response.data);
          this.$router.push("/movies");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
