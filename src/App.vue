<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import AppMovies from "./components/AppMovies.vue";
import AppTvSeries from "./components/AppTvSeries.vue";
import axios from "axios";
import { store } from "./store";

export default {
  data() {
    return {
      store,
    };
  },

  components: {
    AppHeader,
    AppMain,
    AppMovies,
    AppTvSeries,
  },

  methods: {
    RequestDataToApi() {
      axios
        .get("https://api.themoviedb.org/3/search/movie", {
          params: {
            api_key: "eb23ddad3aedd7c42657c036d4ffbb5d",
            query: this.store.SearchBar,
          },
        })
        .then((response) => (this.store.ArrMovies = response.data.results));

      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: "eb23ddad3aedd7c42657c036d4ffbb5d",
            query: this.store.SearchBar,
          },
        })
        .then((response) => (this.store.ArrTvSeries = response.data.results));
    },
  },
  created() {
    axios
      .get('https://api.themoviedb.org/3/movie/popular', {
        params: {
          api_key: 'eb23ddad3aedd7c42657c036d4ffbb5d'
        }
      })
      .then(response => (this.store.ArrMovies = response.data.results));

    axios
      .get('https://api.themoviedb.org/3/tv/popular', {
        params: {
          api_key: 'eb23ddad3aedd7c42657c036d4ffbb5d'
        }
      })
      .then(response => (this.store.ArrTvSeries = response.data.results));
  }
};

</script>

<template>
  <AppHeader @performSearch="RequestDataToApi" />
  <AppMain />
</template>

<style lang="scss">

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
