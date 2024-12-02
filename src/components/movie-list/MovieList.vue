<template>
  <ul class="movie-list list-group">
    <MovieListItem v-for="movie in movies" :movi="movie" />
  </ul>
</template>
<script>
import MovieListItem from "../movie-list-item/MovieListItem.vue";

export default {
  components: {
    MovieListItem,
  },
  data() {
    return {
      movies: [
        { title: "Inception", releaseYear: 2010, favourite: false, like: true },
        {
          title: "The Matrix",
          releaseYear: 1999,
          favourite: false,
          like: false,
        },
        {
          title: "Interstellar",
          releaseYear: 2014,
          favourite: true,
          like: false,
        },
      ],
    };
  },
};
</script>
<style scoped>
.movie-list {
  padding: 1.5rem;
  padding-top: 2rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
