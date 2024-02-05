<template>
  <div>
    <MovieList />
  </div>

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
  }
};
</script>
