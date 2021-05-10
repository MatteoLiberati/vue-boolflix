<template>
  <div class="card">
    <h3>{{ item.title }}{{ item.name }}</h3>
    <h3>{{ item.original_title }} {{ original_name }}</h3>
    <img
      v-if="item.original_language == 'it'"
      src="../assets/img/it.png"
      alt="Italy"
    />
    <img
      v-if="item.original_language == 'en'"
      src="../assets/img/en.png"
      alt="English"
    />
    <span v-else>{{ item.original_language }}</span>
    <!-- <span>{{ item.original_language }}</span> -->
    <div>{{ item.vote_average }}</div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["item"],
};
</script>

<style scoped lang="scss"></style>
