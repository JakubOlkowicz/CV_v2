<template>
  <section class="content">
    <Nuxt />
  </section>
</template>
<script>
export default {
  name: "Content",
};
</script>
<style lang="scss">
@import "@/assets/scss/sections/_content.scss";
.page-enter-active {
  animation: scale 700ms reverse;
}
.page-leave-active {
  animation: scale 700ms;
}
@keyframes scale {
  from {
    transform: scaleX(1);
    transform-origin: left;
    transition: all linear;
    opacity: 1;
  }
  to {
    transform: scaleX(0);
    transform-origin: left;
    transition: all linear;
    opacity: 0;
  }
}
</style>
