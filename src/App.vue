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
    <Start v-if="start" />
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
    };
  },
  computed: {
    getListMovie() {
      // MOVIELIST
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=08725e8c8f7229c5f54f717ccd2e6afb&query=${this.search}&language=it-IT `
        )
        .then((res) => {
          this.movieList = res.data.results;
          this.start = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    getListtv() {
      // TVLIST
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=08725e8c8f7229c5f54f717ccd2e6afb&query=${this.search}&language=it-IT `
        )
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
      this.getListMovie;
      this.getListtv;
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
