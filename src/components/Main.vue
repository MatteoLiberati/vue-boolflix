<template>
  <main class="container">
    <!-- MOVIES -->
    <section v-if="movie.length != 0" class="container-movies">
      <h2>Movies</h2>
      <div class="movies">
        <Card
          :item="element"
          v-for="(element, index) in movie"
          :key="index + element"
        />
      </div>
    </section>

    <!-- TV -->
    <section v-if="tv.length != 0" class="container-series">
      <h2>Series</h2>
      <div class="tv-series">
        <Card
          :item="element"
          v-for="(element, index) in tv"
          :key="index + element"
        />
      </div>
    </section>

    <!-- ELSE -->
    <NoResult v-else />
  </main>
</template>

<script>
// IMPORT
import Card from "@/components/Card";
import NoResult from "@/components/NoResult";
export default {
  name: "Main",
  components: {
    Card,
    NoResult,
  },
  props: ["movie", "tv"],
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/vars.scss";
@import "@/styles/mixins.scss";

// STYLE
main {
  height: 100vh;
  width: 100%;
  @include flex(column);
  section {
    h2 {
      margin: 20px 0;
      text-align: center;
      text-transform: uppercase;
      color: $primary-color;
    }
    .movies,
    .tv-series {
      margin: 50px 0;
      @include flex(vertical);
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
