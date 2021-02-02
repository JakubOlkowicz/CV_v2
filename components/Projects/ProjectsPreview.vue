<template>
  <div class="wrap-item">
    <nuxt-link
      class="item"
      :event="onMake ? '' : 'click'"
      :to="slug"
      :class="{ isDisable: onMake }"
    >
      <div class="text">
        <h3>{{ title }}</h3>
      </div>
      <div class="badge-overlay" :class="{ isDisable: onMake }">
        <span class="top-left badge orange">under building</span>
      </div>
      <img :src="thumbnailUrl" alt="" />
    </nuxt-link>
  </div>
</template>
<script>
export default {
  name: "ProjectsPreview",
  props: {
    title: {
      type: String,
      required: true,
    },
    thumbnailUrl: {
      type: String,
      required: true,
    },
    slug: {
      type: String,
      required: true,
    },
    onMake: {
      type: Boolean,
      required: false,
    },
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/articles/_projects.scss";
</style>
