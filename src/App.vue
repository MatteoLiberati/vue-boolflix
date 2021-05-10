<template>
  <div id="app">
    <Header @search="UserInput">
      <!-- SLOT -->
      <img src="@/assets/img/logoBoolflix.png" alt="" />
    </Header>
  </div>
</template>

<script>
// IMPORT
import Header from "@/components/Header";

export default {
  name: "App",
  components: {
    Header,
  },
  methods: {
    UserInput(userSearch) {
      console.log(userSearch);
    },
  },
};
</script>

<style lang="scss">
@import "@/styles/general.scss";
</style>
