<template>
  <header class="container my-20">
    <!-- SLOT CONENTE LOGO MODIFICABILE IN APPVUE -->
    <slot></slot>
    <div class="right">
      <Menu
        @clickHome="$emit('clickHome')"
        @inspiration="$emit('inspiration')"
      />
      <Input @search="input" />
    </div>
  </header>
</template>

<script>
import Input from "@/components/Input";
import Menu from "@/components/Menu";
export default {
  name: "Header",
  components: {
    Input,
    Menu,
  },
  data() {
    return {};
  },
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
@import "@/styles/mixins";

// STYLE
header {
  width: 100%;
  @include flex("space-bet-v");
  @media screen and (max-width: 1000px) {
    @include flex(column);
  }
  .right {
    @include flex(vertical);
    @media screen and (max-width: 698px) {
      @include flex(column);
    }
  }
}
</style>
