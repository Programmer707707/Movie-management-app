<template>
  <div class="app">
    <div class="content">
      <AppInfo
        :allMoviesCount="movies.length"
        :favouriteCount="movies.filter((c) => c.favorite).length"
      />

      <div class="search-panel">
        <SearchPanel :updateTermHandler="updateTermHandler" />
        <AppFilter
          :updateFilterHandler="updateFilterHandler"
          :filterName="filter"
        />
      </div>

      <MovieList
        v-if="movies.length"
        :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onDelete="onDeleteHandler"
      />

      <div v-else-if="isLoading">
        <Loader />
      </div>

      <Box v-else>
        <p class="text-center fs-5">Movies are not availabe ❌</p>
      </Box>

      <Box class="d-flex justify-content-center">
        <Pagination
          :totalPage="totalPage"
          :page="page"
          @onChangePageHandler="changePageHandler"
        />
      </Box>

      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
import AppFilter from "../app-filter/AppFilter.vue";
import AppInfo from "../app-info/AppInfo.vue";
import MovieAddForm from "../movie-add-form/MovieAddForm.vue";
import MovieList from "../movie-list/MovieList.vue";
import PrimaryButton from "../ui-components/PrimaryButton.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
import axios from "axios";
import Loader from "../ui-components/Loader.vue";
import Pagination from "../ui-components/Pagination.vue";

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
      movies: [],
      term: "",
      filter: "",
      isLoading: false,
      limit: 10,
      page: 1,
      totalPage: 0,
    };
  },
  //Methods to use for general purpose
  methods: {
    //Synchronous function to add a new movie
    async createMovie(item) {
      const response = await axios.post(
        "https://jsonplaceholder.typicode.com/posts",
        item
      );
      this.movies.push(response.data);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },

    async onDeleteHandler(id) {
      const res = await axios.delete(
        `https://jsonplaceholder.typicode.com/posts/${id}`
      );
      this.movies = this.movies.filter((c) => c.id !== id);
    },

    onSearchHandler(arr, term) {
      if (term.length == 0) {
        return arr;
      }
      return arr.filter((c) => c.name.toLowerCase().indexOf(term) > -1);
    },

    onFilterHandler(arr, filter) {
      switch (filter) {
        case "like":
          return arr.filter((c) => c.like);
        case "mostViewers":
          return arr.filter((c) => c.viewers > 500);
        default:
          return arr;
      }
    },

    updateTermHandler(term) {
      this.term = term;
    },

    updateFilterHandler(filter) {
      this.filter = filter;
    },

    //Fetched api using axios and used try,catch block
    async fetchMovie() {
      try {
        this.isLoading = true;

        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts?",
          {
            params: {
              _limit: this.limit,
              _page: this.page,
            },
          }
        );
        const newArr = response.data.map((item) => ({
          id: item.id,
          name: item.title,
          like: false,
          favorite: false,
          viewers: item.id * 100 - 3,
        }));
        this.totalPage = Math.ceil(
          response.headers["x-total-count"] / this.limit
        );
        this.movies = newArr;
      } catch (error) {
        alert(error);
      } finally {
        this.isLoading = false;
      }
    },

    changePageHandler(page) {
      this.page = page;
      this.fetchMovie();
    },
  },

  //Lifecycle methods
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
  color: black;
}
.content {
  width: 1000px;
  min-height: 700px;
  background-color: #ffffff;
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
