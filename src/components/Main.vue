<template>
  <main class="container">
    <!-- MOVIES -->
    <section
      v-if="movie.length !== 0 && openIspiration == false"
      class="container-movies"
    >
      <h2>Movies</h2>
      <div class="movies cards-shadow container">
        <Card
          :item="element"
          v-for="(element, index) in movie"
          :key="index + element"
        />
      </div>
    </section>

    <!-- TV -->
    <section
      v-if="tv.length !== 0 && openIspiration == false"
      class="container-series"
    >
      <h2>Series</h2>
      <div class="tv-series cards-shadow container">
        <Card
          :item="element"
          v-for="(element, index) in tv"
          :key="index + element"
        />
      </div>
    </section>

    <!-- ELSE -->
    <NoResult
      @search="input"
      v-show="movie.length == 0 && tv.length == 0 && openIspiration == false"
    />
    <Inspiration v-show="openIspiration" :bestMovie="best" />
  </main>
</template>

<script>
// IMPORT
import Card from "@/components/Card";
import NoResult from "@/components/NoResult";
import Inspiration from "@/components/Inspiration";

export default {
  name: "Main",
  components: {
    Card,
    NoResult,
    Inspiration,
  },
  props: ["movie", "tv", "openIspiration", "best"],
  methods: {
    /**
     * RI-EMIT DELL'INPUT
     */
    input(item) {
      this.$emit("search", item);
    },
  },
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/vars.scss";
@import "@/styles/mixins.scss";

// STYLE
main {
  position: relative;
  flex-grow: 1;
  width: 100%;

  section {
    @include flex(column-center);
    h2 {
      margin: 20px 0;
      text-align: center;
      text-transform: uppercase;
      color: $primary-color;
    }

    .movies,
    .tv-series {
      @include flex(flex);
      overflow-x: auto;
      @media screen and (max-width: 800px) {
        height: 500px;
        overflow-y: auto;
        flex-wrap: wrap;
        justify-content: center;
      }
    }
  }
}
</style>
