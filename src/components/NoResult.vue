<template>
  <div class="no-result">
    <div class="layover"></div>
  </div>
</template>

<script>
export default {
  name: "NoResult",
};
</script>

<style scoped lang="scss">
// @import "@/styles/mixins";

.no-result {
  width: 100%;
  flex-grow: 1;
  background-image: url("../assets/img/start-cover.jpg");
  //   .layover {
  //     width: 100%;
  //     height: 100%;
  //     @include flex(center);
  //     background-color: rgba($secondary-color, 0.3);
  //   }
}
</style>
