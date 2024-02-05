<template>
  <div class="movieList">
    <!-- list of movies -->
    <v-row>
      <v-col
        v-for="movie in movies.results"
        :key="movie.id"
        cols="12"
        sm="6"
        md="4"
        lg="4"
      >
        <v-card>
          <v-img :src="photo_path + movie.poster_path" alt="movie poster" />
          <h3>{{ movie.title }}</h3>
        </v-card>
      </v-col>
    </v-row>
    <!-- <ul>
      <li v-for="movie in movies.results">
        <v-card>
            <img :src="photo_path + movie.poster_path" alt="movie poster" />
            <h3 class="movieList">{{ movie.title }}</h3>
        </v-card>
      </li>
    </ul> -->
  </div>
</template>

<script>
const config = require("../config.json");
import axios from "axios";

export default {
  name: "MoviesList",
  data() {
    return {
      movies: [],
      photo_path: config.url.photo_path,
    };
  },
  mounted() {
    axios
      .get(config.url.movie_list, {
        headers: {
          Authorization: `bearer ${config.api_key}`,
        },
      })
      .then((response) => {
        this.movies = response.data;
        console.log(this.movies.results);
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style>
.movieList h3 {
  /* border-bottom: 1px solid rgb(55, 0, 255); */
  text-align: center;
  margin: auto 1em;
  padding: 1em 0;
  color: white;
}

.movieList ul {
  list-style-type: none;
  display: inline-flex;
  flex-wrap: wrap;
}

.movieList li {
  /* border: 3px solid rgb(55, 0, 255); */
  margin: 5px 5px;
  background: #bac2d7;
  border-radius: 10px;
}

.movieList img {
  padding-top: 10px;
  width: 150px;
}
</style>
