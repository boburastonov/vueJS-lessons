<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
        :allMoviesCount="movies.length"
        :favouriteMoviesCount="movies.filter((m) => m.favourite).length"
      />
      <div class="search-panel">
        <SearchPanel :onUpdateTermHandler="onUpdateTermHandler" />
        <AppFilter
          :onUpdateFilterHandler="onUpdateFilterHandler"
          :filterName="filter"
        />
      </div>
      <Box v-if="!movies.length && !isLoading">
        <p class="text-center text-danger fs-3">Kinolar mavjud emas</p>
      </Box>
      <Box class="d-flex justify-content-center" v-else-if="isLoading">
        <Loader />
      </Box>
      <MovieList
        v-else
        :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onDelete="deleteHandler"
      />
      <Box class="d-flex justify-content-end">
        <Pagination
          :totalPages="totalPages"
          :page="page"
          @update:page="onPageChange"
        />
      </Box>
      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AppInfo from "../app-info/AppInfo.vue";
import AppFilter from "../app-filter/AppFilter.vue";
import MovieList from "../movie-list/MovieList.vue";
import Pagination from "../Pagination/Pagination.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
import MovieAddForm from "../movie-add-form/MovieAddForm.vue";

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
    Pagination,
  },
  data() {
    return {
      movies: [],
      term: "",
      filter: "all",
      isLoading: false,
      limit: 10,
      page: 1,
      totalPages: 0,
    };
  },
  methods: {
    async createMovie(movie) {
      try {
        const response = await axios.post(
          "https://jsonplaceholder.typicode.com/posts",
          movie
        );
        this.movies.push(response.data);
      } catch (error) {
        alert(error.message);
      }
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
    async deleteHandler(id) {
      try {
        const response = await axios.delete(
          `https://jsonplaceholder.typicode.com/posts/${id}`
        );
        this.movies = this.movies.filter((item) => item.id !== id);
      } catch (error) {
        alert(error.message);
      }
    },
    onSearchHandler(arr, term) {
      if (term.length === 0) return arr;
      return arr.filter((item) =>
        item.title.toLowerCase().includes(term.toLowerCase())
      );
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter((item) => item.like);
        case "mostViewers":
          return arr.filter((item) => item.viewers > 713);
        default:
          return arr;
      }
    },
    onUpdateTermHandler(term) {
      this.term = term;
    },
    onUpdateFilterHandler(filter) {
      this.filter = filter;
    },
    onPageChange(newPage) {
      this.page = newPage;
      this.fetchMovie();
    },
    async fetchMovie() {
      try {
        this.isLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _limit: this.limit,
              _page: this.page,
            },
          }
        );
        const newArr = response.data.map((item) => ({
          id: item.id,
          title: item.title,
          like: false,
          favourite: false,
          viewers: item.id * 100,
        }));
        this.totalPages = Math.ceil(
          response.headers["x-total-count"] / this.limit
        );
        this.movies = newArr;
      } catch (error) {
        alert(error.message);
      } finally {
        this.isLoading = false;
      }
    },
  },
  mounted() {
    this.fetchMovie();
  },
  watch: {
    page() {
      this.fetchMovie();
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
