<template>
  <section>
    <h2 class="mb-20 text-center">
      Lasciati ispirare dai alcuni dei nostri film più visti
    </h2>
    <div class="container-cards">
      <Card
        :item="element"
        v-for="(element, index) in bestMovie"
        :key="element.name + index"
      />
    </div>
  </section>
</template>

<script>
import Card from "@/components/Card";
export default {
  name: "Inspiration",
  components: {
    Card,
  },
  props: ["bestMovie"],
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/vars";
@import "@/styles/mixins";

// STYLE
section {
  position: absolute;
  padding: 50px;
  width: 100%;
  min-height: 100%;
  background-color: $secondary-color;
  h2 {
    text-shadow: 0px 0px 2px #fff;
    font-size: 2rem;
    color: $primary-color;
  }
  .container-cards {
    @include flex(horizontal);
    flex-wrap: wrap;
  }
}
</style>
