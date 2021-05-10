<template>
  <main class="container">
    <!-- MOVIES -->
    <section class="movies">
      <Card
        :item="element"
        v-for="(element, index) in movie"
        :key="index + element"
      />
    </section>
    <hr />
    <!-- TV -->
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

<style scoped lang="scss"></style>
