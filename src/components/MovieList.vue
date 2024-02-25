<template>
  <!-- list of movies -->
  <v-row>
    <v-col v-for="movie in movieFiltered.results" :key="movie.id" cols="3">
      <v-card class="mx-auto" max-width="auto" height="475" theme="dark">
        <v-container>
          <v-row>
            <v-col>
              <v-img
                height="300px"
                :src="photo_path + movie.poster_path"
                alt="movie poster"
              ></v-img>
              <v-card-title class="text-h5">{{ movie.title }}</v-card-title>
              <v-card-text class="text-subtitle-1">
                <!-- truncate -->
                <p>
                  <!-- {{ movie.overview.length > 45
                    ? movie.overview.substring(0, 45) + "..."
                    : movie.overview }} -->
                  {{
                    movie.overview.length < 1
                      ? movie.overview +
                        "______________________________________"
                      : movie.overview.substring(0, 40) + "..."
                  }}
                </p>
              </v-card-text>
              <v-card-actions>
                <v-btn
                  class="text font-weight-bold"
                  color="teal-accent-4"
                  @click="sendMovie(movie.id)"
                  >Plus d'informations
                </v-btn>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
const config = require("../config.json");
import axios from "axios";
import _ from "lodash";

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
        console.log(response.data.results);
      })
      .catch((error) => {
        console.log(error);
      });
  },
  methods: {
    sendMovie(id) {
      this.$emit("showMovieDetailEmit", id);
    },
  },
  props: {
    search: String,
  },
  computed: {
    movieFiltered: function () {
      // return this.movies.filter((movie) => {
      //   return movie.title.toLowerCase().includes(this.search.toLowerCase());
      // });
      return _.filter(this.movies, (movie) => {
        return movie.title.toLowerCase().includes(this.search.toLowerCase());
      });
      // return this.movies;
    },
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
