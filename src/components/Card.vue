<template>
  <!-- CARD UTILIZZATA SIA PER LA LISTA FILM CHE PER LA LISTA SERIE TV -->
  <div v-if="item" @mouseenter="content" @mouseleave="content" class="card">
    <div class="cover">
      <img :src="poster(item.poster_path)" :alt="item.title + item.name" />
      <!-- TITOLO VISIBILE SOLO SE L'IMMAGINE DI COVER NON E' DISPONIBILE,
      VERRA' GENERATA L'IMMAGINE SOSTITUTIVA E IL TITOLO SERVIRA' PER DISTINGUERE IL
      CONTENUTO ALTRIMENTI VISIBILE SOLO ALL'HOVER -->
      <div class="text-nocover text-center" v-show="item.poster_path == null">
        <h2>{{ item.title }}{{ item.name }}</h2>
      </div>
    </div>

    <!-- CONTENT CARD VISIBILE SOLO ALL'HOVER SULLA COVER-->
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
        <!-- STAMPA LE BANDIERE CON LE SIGLE DELLE LINGUE NEL CASO L'ARRAY FLAGS
        CONTENGA LE SIGLE RESTITUITE DALL'ORIGINAL LANGUAGE -->
        <img
          v-if="this.flags.includes(item.original_language)"
          :src="require(`@/assets/img/${item.original_language}.png`)"
          :alt="item.original_language"
        />
        <span v-else>{{ item.original_language }}</span>
      </div>

      <!-- VOTE -->
      <div class="vote">
        <!-- FULL STARS -->
        <i
          class="fas fa-star"
          v-for="(element, index) in ceil(item.vote_average)"
          :key="'full' + index"
        ></i>

        <!-- EMPTY STARS -->
        <i
          class="far fa-star"
          v-for="(element, index) in 5 - ceil(item.vote_average)"
          :key="'empty' + index"
        ></i>
      </div>

      <!-- TRAMA -->
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
      flags: ["it", "en"],
    };
  },
  methods: {
    /**
     * MODIFICA IL VALORE DI VALUTAZIONE DA 1 A 10
     * IN SCALA DA 1 A 5
     * E RITORNA IL VALORE ARROTONDANDOLO AL VALORE INTERO
     * PIU' ALTO
     */
    ceil(number) {
      number = number / 2;
      return Math.ceil(number);
    },
    /**
     * IN IF STAMPA L'IMMAGINE POSTER
     * IN ELSE NEL CASO DI RISULTATO SENZA IMMAGINE POSTER
     * STAMPA AL SUO POSTO UN IMMAGINE "NO IMAGE AVAILABLE"
     */
    poster(link) {
      if (link != null) {
        return `https://image.tmdb.org/t/p/w342/${link}`;
      } else {
        return `https://www.tropposmart.it/themes/AngarTheme/assets/img/en-default-large_default.jpg`;
      }
    },
    /**
     * IN MOUSEENTER E MOUSELEAVE RENDE VISIBILE O MENO IL CONTENUTO ABSOLUTE
     */
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
    position: relative;
    img {
      height: 513px;
      width: 342px;
      object-fit: cover;
      border: 1px solid rgba($secondary-color, 0.5);
      cursor: pointer;
      @media screen and (max-width: 1270px) {
        height: 300px;
        width: 200px;
      }
      @media screen and (max-width: 700px) {
        height: 150px;
        width: 100px;
      }
    }
    .text-nocover {
      position: absolute;
      top: 0;
      left: 0;
      padding: 20px;
      height: 100%;
      width: 100%;
      color: $secondary-color;
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
    background-color: rgba($secondary-color, 0.6);
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
