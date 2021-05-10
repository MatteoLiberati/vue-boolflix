<template>
  <header class="container">
    <slot></slot>
    <div class="input">
      <input @keyup.enter="search" v-model.trim="userSearch" type="text" />
      <button @click="search">Cerca</button>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      userSearch: "",
    };
  },
  methods: {
    search() {
      this.$emit("search", this.userSearch);
      this.userSearch = "";
    },
  },
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/mixins";
// STYLE
header {
  @include flex("space-bet-v");
}
</style>
