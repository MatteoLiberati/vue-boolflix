<template>
  <ul>
    <a href="#">
      <li @click="$emit('clickHome')">Home</li>
    </a>
    <a href="#">
      <li @click="$emit('inspiration')">Lasciati ispirare</li>
    </a>
  </ul>
</template>
<script>
export default {
  name: "Menu",
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/mixins";
@import "@/styles/vars";
// STYLE
ul {
  @include flex(flex);
  list-style: none;
  @media screen and (max-width: 698px) {
    margin-bottom: 20px;
  }
  a {
    text-decoration: none;
    color: $text-color;
    margin-right: 20px;
    text-transform: uppercase;
  }
}
</style>
