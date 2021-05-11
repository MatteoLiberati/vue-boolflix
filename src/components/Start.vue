<template>
  <div class="start container">
    <div class="layover">
      <div class="content-start">
        <h1 class="mb-20">Benvenuto su Boolflix</h1>
        <span class="mb-10">Inizia subito l'esperienza</span>
        <span>Cerca il film o la tua serie preferita</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Start",
};
</script>

<style scoped lang="scss">
// IMPORT
@import "@/styles/mixins";
@import "@/styles/vars";

// STYLE
.start {
  width: 100%;
  flex-grow: 1;
  background-image: url("../assets/img/start-cover.jpg");
  .layover {
    width: 100%;
    height: 100%;
    @include flex(center);
    background-color: rgba($secondary-color, 0.3);
    .content-start {
      font-size: 1.2rem;
      @include flex(column);
      text-align: center;
      border-radius: 8px;
    }
  }
}
</style>
