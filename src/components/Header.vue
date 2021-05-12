<template>
  <header class="container my-20">
    <slot></slot>
    <Input @search="input" />
  </header>
</template>

<script>
import Input from "@/components/Input";
export default {
  name: "Header",
  components: {
    Input,
  },
  data() {
    return {};
  },
  methods: {
    input(item) {
      this.$emit("search", item);
    },
  },
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/mixins";

// STYLE
header {
  width: 100%;
  @include flex("space-bet-v");
  @media screen and (max-width: 700px) {
    @include flex(column);
  }
}
</style>
