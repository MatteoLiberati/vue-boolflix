<template>
  <div id="app">
    <!-- HEADER -->
    <Header @clickHome="home" @search="userInput" @inspiration="inspiration">
      <!-- SLOT CON LOGO -->
      <a href="#"
        ><img @click="home" src="@/assets/img/logoBoolflix.png" alt="logo"
      /></a>
    </Header>

    <!-- START BEFORE SEARCH -->
    <Start @search="userInput" :best="bestMovies" v-if="start" />

    <!-- MAIN -->
    <Main @search="userInput" v-else :movie="movieList" :tv="tvList" />
    <Inspiration v-show="sectionInspiration" />
  </div>
</template>

<script>
// IMPORT
import Header from "@/components/Header";
import Main from "@/components/Main";
import Start from "@/components/Start";
import Inspiration from "@/components/Inspiration";
import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    Main,
    Start,
    Inspiration,
  },
  data() {
    return {
      lastSearch: "",
      movieList: [],
      bestMovies: [],
      tvList: [],
      sectionInspiration: false,
      chars: "abcdefghijklmnopqrstuvwxyz",
      start: true,
      apiUrl: "https://api.themoviedb.org/3/search/",
      apiKey: "08725e8c8f7229c5f54f717ccd2e6afb",
    };
  },
  mounted() {
    this.bestMovieRandom();
  },
  methods: {
    /**
     * se la parola ricercata non è uguale a quella precedente
     * ed è diversa da una stringa vuota
     * esegue una chiamata ajax usando come query la parola scritta
     * e associa gli array movieList e tvList a quelli presenti nella api
     */
    userInput(userSearch) {
      if (this.lastSearch !== userSearch && userSearch != "") {
        this.lastSearch = userSearch;
        const apiParams = {
          api_key: this.apiKey,
          query: userSearch,
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
      }
    },
    /**
     * genera una lettera a caso per l'array bestMovies
     */
    randomChars() {
      let char = this.chars.charAt(
        Math.floor(Math.random() * this.chars.length)
      );
      return char;
    },
    /**
     * al click del logo presente in header
     * riapre la facciata di start iniziale
     * coprendo tutto il resto del main
     */
    home() {
      this.start = true;
      this.bestMovieRandom();
    },
    /**
     * Aggiorna l'array movie ricercando un carattere a caso
     */
    bestMovieRandom() {
      //BESTMOVIE RANDOM
      axios
        .get(this.apiUrl + "movie", {
          params: {
            api_key: this.apiKey,
            query: this.randomChars(),
          },
        })
        .then((res) => {
          this.bestMovies = res.data.results.filter((element) => {
            return element.vote_average > 7;
          });
        })
        .catch((err) => {
          console.log(err);
        });
    },
    inspiration() {
      this.sectionInspiration = true;
    },
  },
};
</script>

<style lang="scss">
// STYLE GENERALE
@import "@/styles/general.scss";
</style>
