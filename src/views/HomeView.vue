<template>
  <MovieList @showMovieDetailEmit="showMovieDetailEmit" />
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
    };
  },
  methods: {
    showMovieDetailEmit(movieId) {
      this.movieId = movieId;
      this.showMovieDetail = true;
    },
    closeDetail() {
      this.showMovieDetail = false;
    },
  },
};
</script>
