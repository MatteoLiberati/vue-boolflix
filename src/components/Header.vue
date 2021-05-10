<template>
  <header class="container">
    <slot></slot>
    <div class="input">
      <input v-model="userSearch" type="text" />
      <button @click="$emit('search', userSearch)">Cerca</button>
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
