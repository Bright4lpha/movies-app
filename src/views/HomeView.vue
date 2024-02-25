<template>
  <v-container>
    <v-row>
      <v-col>
        <MovieSearch @searchMovieEmit="setMovieEmit" />
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <MoviePagination />
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <MovieList @showMovieDetailEmit="showMovieDetailEmit" />
      </v-col>
    </v-row>
  </v-container>
  <MovieDetail v-if="showMovieDetail" :movieId="movieId" @close="closeDetail" />
</template>

<script>
import MovieList from "@/components/MovieList";
import MoviePagination from "@/components/MoviePagination";
import MovieDetail from "@/components/MovieDetail";
import MovieSearch from "@/components/MovieSearch";
export default {
  name: "HomeView",
  components: {
    MovieList,
    MoviePagination,
    MovieDetail,
    MovieSearch,
  },

  data() {
    return {
      movieId: null,
      showMovieDetail: false,
      search: null,
    };
  },
  props: {
    search: String,
  },
  methods: {
    showMovieDetailEmit(movieId) {
      this.movieId = movieId;
      this.showMovieDetail = true;
    },
    closeDetail() {
      this.showMovieDetail = false;
    },
    setMovieEmit(search) {
      this.search = search;
      console.log(this.search);
    },
  },
};
</script>
