<template>
  <div class="list">
    <span>{{ data }}</span>
    <h3>{{ place }}</h3>
    <span>{{ town }}</span>
    <p>{{ doing }}</p>
  </div>
</template>
<script>
export default {
  name: "JobsList",
  props: {
    data: {
      type: String,
      required: true,
    },
    place: {
      type: String,
      required: true,
    },
    town: {
      type: String,
      required: true,
    },
    doing: {
      type: String,
      required: true,
    },
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/articles/_jobs.scss";
</style>
