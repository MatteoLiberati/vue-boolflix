<template>
  <div @mouseenter="content" @mouseleave="content" class="card">
    <div class="cover">
      <img :src="poster(item.poster_path)" :alt="item.title + item.name" />
    </div>
    <!-- CONTENT CARD -->
    <div v-show="showContent" class="content-card">
      <h2 class="mb-10 text-center">{{ item.title }}{{ item.name }}</h2>
      <!-- ORIGINAL TITLE -->
      <div class="original-title mb-20">
        <span class="mr-8 primary">Titolo originale:</span>
        <span> {{ item.original_title }}{{ item.original_name }} </span>
      </div>
      <!-- LANGUAGE -->
      <div class="language mb-10">
        <span class="mr-8 primary">lingua originale:</span>
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
      </div>
      <!-- VOTE -->
      <div class="vote">
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
      <div class="plot">
        <span class="mb-10 primary">trama:</span>
        <span>{{ item.overview }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["item"],
  data() {
    return {
      showContent: false,
    };
  },
  methods: {
    ceil(number) {
      number = number / 2;
      return Math.ceil(number);
    },
    poster(link) {
      if (link != null) {
        return `https://image.tmdb.org/t/p/w500/${link}`;
      } else {
        return `https://upload.wikimedia.org/wikipedia/commons/b/b9/No_Cover.jpg`;
      }
    },
    content() {
      this.showContent = !this.showContent;
    },
  },
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/vars";
@import "@/styles/mixins";
// STYLE
.card {
  position: relative;
  .cover {
    img {
      height: 400px;
      width: 350px;
      object-fit: cover;
      border: 1px solid rgba($secondary-color, 0.5);
      cursor: pointer;
      @media screen and (max-width: 1270px) {
        height: 300px;
        width: 250px;
      }
      @media screen and (max-width: 700px) {
        height: 220px;
        width: 180px;
      }
    }
  }
  .content-card {
    position: absolute;
    padding: 20px;
    overflow-y: auto;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    background-color: rgba($secondary-color, 0.5);
    @include flex(column);
    cursor: pointer;
    // LANGUAGE
    .language {
      @include flex(vertical);
      & > img {
        height: 1rem;
      }
      // VOTE
    }
    .vote {
      text-align: right;
      color: yellow;
    }
    // PLOT
    .plot {
      @include flex(column);
    }
  }
}
</style>
