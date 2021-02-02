<template>
  <section class="me">
    <div class="img">
      <div class="text">
        <h3>{{ me }}</h3>
        <span>{{ jobs }}</span>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "Me",
  data() {
    return {
      me: "jakub olkowicz",
      jobs: "junior developer",
    };
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/sections/_me.scss";
</style>
