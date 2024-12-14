<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
        :allMoviesCount="movies.length"
        :favouriteMoviesCount="movies.filter((m) => m.favourite).length"
      />
      <div class="search-panel">
        <SearchPanel />
        <AppFilter />
      </div>
      <MovieList :movies="movies" @onToggle="onToggleHandler" />
      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>
<script>
import AppInfo from "../app-info/AppInfo.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
import AppFilter from "../app-filter/AppFilter.vue";
import MovieList from "../movie-list/MovieList.vue";
import MovieAddForm from "../movie-add-form/MovieAddForm.vue";
export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
  },
  data() {
    return {
      movies: [
        {
          title: "Inception",
          viewers: 716,
          favourite: false,
          like: true,
          id: 1,
        },
        {
          title: "The Matrix",
          viewers: 719,
          favourite: false,
          like: false,
          id: 2,
        },
        {
          title: "Interstellar",
          viewers: 713,
          favourite: true,
          like: false,
          id: 3,
        },
      ],
    };
  },
  methods: {
    createMovie(movie) {
      this.movies.push(movie);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id == id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
  },
};
</script>
<style>
.app {
  height: 100vh;
  color: #000;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
