<template>
  <!-- STARTER INIZIALE E RIAPRIBILE CON CLICK SU LOGO IN HEADER -->
  <div class="start container">
    <!-- LAYOVER OPACO CON TRASPARENZA -->
    <div class="layover">
      <div class="content-start">
        <h1 class="mb-20">Benvenuto su Boolflix</h1>
        <span class="mb-10">Inizia subito l'esperienza</span>
        <span class="mb-10">Cerca il film o la tua serie preferita</span>
        <Input class="mb-20" @search="input" />
        <h2 class="mb-20">I nostri utenti consigliano:</h2>
        <div class="listBestMovie cards-shadow">
          <Card
            v-for="(item, index) in recommended(best)"
            :key="index + 'key'"
            :item="item"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Input from "@/components/Input";
import Card from "@/components/Card";
export default {
  name: "Start",
  components: {
    Input,
    Card,
  },
  props: ["best"],
  methods: {
    /**
     * RI-EMIT DELL'INPUT
     */
    input(item) {
      this.$emit("search", item);
    },
    recommended(best) {
      let newArray = [];
      for (let i = 0; i < 3; i++) {
        newArray.push(best[i]);
      }
      return newArray;
    },
  },
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/mixins";
@import "@/styles/vars";

// STYLE
.start {
  @include flex(column);
  width: 100%;
  flex-grow: 1;
  background-image: url("../assets/img/start-cover.jpg");

  .layover {
    width: 100%;
    height: 100%;
    @include flex(center);
    background-color: rgba($secondary-color, 0.35);

    .content-start {
      font-size: 1.2rem;
      @include flex(column);
      text-align: center;
      border-radius: 8px;
    }
    h2 {
      text-shadow: 0px 0px 2px $text-color;
      color: $primary-color;
    }
    .listBestMovie {
      @include flex(flex);
    }
  }
}
</style>
