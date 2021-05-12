<template>
  <div id="app">
    <!-- HEADER -->
    <Header @search="userInput">
      <!-- SLOT -->
      <a href="#"
        ><img @click="home" src="@/assets/img/logoBoolflix.png" alt="logo"
      /></a>
    </Header>
    <!-- START BEFORE SEARCH -->
    <Start @search="userInput" v-if="start" />
    <!-- MAIN -->
    <Main v-else :movie="movieList" :tv="tvList" />
  </div>
</template>

<script>
// IMPORT
import Header from "@/components/Header";
import Main from "@/components/Main";
import Start from "@/components/Start";
import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    Main,
    Start,
  },
  data() {
    return {
      search: "",
      movieList: [],
      tvList: [],
      start: true,
      apiUrl: "https://api.themoviedb.org/3/search/",
      apiKey: "08725e8c8f7229c5f54f717ccd2e6afb",
    };
  },
  computed: {
    getList() {
      const apiParams = {
        api_key: this.apiKey,
        query: this.search,
      };
      // MOVIELIST
      axios
        .get(this.apiUrl + "movie", { params: apiParams })
        .then((res) => {
          this.movieList = res.data.results;
          this.start = false;
        })
        .catch((err) => {
          console.log(err);
        });
      // TVLIST
      axios
        .get(this.apiUrl + "tv", { params: apiParams })
        .then((res) => {
          this.tvList = res.data.results;
          this.start = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  methods: {
    userInput(userSearch) {
      this.search = userSearch;
      this.getList;
    },
    home() {
      this.start = true;
    },
  },
};
</script>

<style lang="scss">
@import "@/styles/general.scss";
</style>
