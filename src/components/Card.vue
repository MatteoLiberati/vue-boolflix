<template>
  <div class="card">
    <div class="cover">
      <img
        :src="`https://image.tmdb.org/t/p/w342/${item.backdrop_path}`"
        :alt="item.title + item.name"
      />
    </div>
    <!-- CONTENT CARD -->
    <div class="content-card">
      <h3>{{ item.title }}{{ item.name }}</h3>
      <h3>{{ item.original_title }} {{ item.original_name }}</h3>
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
      <!-- VOTE -->
      <div>{{ ceil(item.vote_average) }}</div>
      <!-- FULL STARS -->
      <i
        class="fas fa-star"
        v-for="(element, index) in ceil(item.vote_average)"
        :key="index + element"
      ></i>
      <!-- EMPTY STARS -->
      <i
        class="far fa-star"
        v-for="(element, index) in 5 - ceil(item.vote_average)"
        :key="'key' + index + element"
      ></i>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["item"],
  methods: {
    ceil(number) {
      console.log(number);
      number = number / 2;
      return Math.ceil(number);
    },
  },
};
</script>

<style scoped lang="scss"></style>
