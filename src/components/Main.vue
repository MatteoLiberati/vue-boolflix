<template>
  <main class="container">
    <!-- MOVIES -->
    <h2>Movies</h2>
    <section class="movies">
      <Card
        :item="element"
        v-for="(element, index) in movie"
        :key="index + element"
      />
    </section>
    <hr />
    <!-- TV -->
    <h2>Series</h2>
    <section class="tv-series">
      <Card
        :item="element"
        v-for="(element, index) in tv"
        :key="index + element"
      />
    </section>
  </main>
</template>

<script>
// IMPORT
import Card from "@/components/Card";
export default {
  name: "Main",
  components: {
    Card,
  },
  props: ["movie", "tv"],
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/mixins.scss";
// STYLE
main {
  h2 {
    margin: 20px 0;
    text-align: center;
  }
  section {
    margin: 50px 0;
    @include flex(vertical);
    overflow-x: auto;
  }
}
</style>
