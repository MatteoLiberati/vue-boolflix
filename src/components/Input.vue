<template>
  <!-- COMPONENTE DI INPUT UTILIZZATO IN HEADER, START E NORESULT -->
  <div class="input">
    <input
      class="mr-8"
      @keyup.enter="search"
      v-model.trim="userSearch"
      type="text"
    />
    <button @click="search">Cerca</button>
  </div>
</template>

<script>
export default {
  name: "Input",
  data() {
    return {
      userSearch: "",
    };
  },
  methods: {
    /**
     * PRIMO EMIT DELL'INPUT
     */
    search() {
      this.$emit("search", this.userSearch);
      this.userSearch = "";
    },
  },
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/vars";
// STYLE
input {
  width: 180px;
  height: 30px;
  border-radius: 10px;
  appearance: none;
  outline: none;
  border: none;
  padding-left: 10px;
  font-size: 1.1rem;
  background-color: $text-color;
  color: $background-color;
  &:focus {
    box-shadow: 0px 0px 2px 2px $primary-color;
  }
}

button {
  padding: 8px 16px;
  border-radius: 8px;
  background-color: $primary-color;
  border: none;
  color: $text-color;
  font-size: 1.1rem;
  cursor: pointer;
  appearance: none;
  outline: none;
  transition: background-color 0.3s;
  &:focus,
  &:hover {
    background-color: rgba($primary-color, 0.8);
  }
}
</style>
