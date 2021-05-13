<template>
  <!-- COMPONENTE IN ELSE QUANDO LA RICERCA NON PRODUCE RISULTATI -->
  <div class="no-result">
    <!-- LAYOVER OPACO CON TRASPARENZA -->
    <div class="layover">
      <h2 class="mb-10">Non è stato trovato alcun risultato</h2>
      <span class="mb-20">Riprova</span>
      <Input @search="input" />
    </div>
  </div>
</template>

<script>
import Input from "@/components/Input";
export default {
  name: "NoResult",
  components: {
    Input,
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
@import "@/styles/mixins";
@import "@/styles/vars";

.no-result {
  width: 100%;
  height: 100%;
  background-image: url("../assets/img/start-cover.jpg");

  .layover {
    width: 100%;
    height: 100%;
    font-size: 1.2rem;
    @include flex("column-center");
    background-color: rgba($secondary-color, 0.35);
  }
}
</style>
