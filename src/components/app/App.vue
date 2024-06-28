<template>
  <div class="app font">
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
        :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onDelete="onDeleteHandler"
      />
      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
import AppFilter from "../app-filter/AppFilter.vue";
import AppInfo from "../app-info/AppInfo.vue";
import MovieAddForm from "../movie-add-form/MovieAddForm.vue";
import MovieList from "../movie-list/MovieList.vue";
import SearchPanel from "../search-panel/SearchPanel.vue";
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
        { name: "Omar", viewers: 811, like: false, favorite: false, id: 1 },
        {
          name: "Spiderman",
          viewers: 411,
          like: true,
          favorite: false,
          id: 2,
        },
        { name: "Batman", viewers: 311, like: false, favorite: false, id: 3 },
        { name: "Joker", viewers: 211, like: false, favorite: false, id: 4 },
      ],
      term: "",
      filter: "",
    };
  },

  methods: {
    createMovie(item) {
      this.movies.push(item);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map((item) => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
    onDeleteHandler(id) {
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
