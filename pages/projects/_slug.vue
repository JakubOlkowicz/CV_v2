<template>
  <article class="projects single">
    <h1 class="title">{{ title }}</h1>
    <div class="pause">
      <p>{{ previewText }}</p>
      <div class="btns">
        <a v-if="live" :href="live" class="btn">live</a>
        <a v-if="github" :href="github" class="btn">githube</a>
      </div>
    </div>
    <masonry
      :cols="{ default: 1 }"
      :gutter="{ default: '10px' }"
      class="container"
    >
      <img :src="thumbnailUrl" alt="" />
    </masonry>
  </article>
</template>

<script>
export default {
  name: "Projects",

  async asyncData({ app, route }) {
    const slug = route.params.slug;
    return app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "projects/",
        by_slugs: "*/" + slug,
      })
      .then((res) => {
        return {
          id: res.data.stories[0].slug,
          title: res.data.stories[0].content.title,
          previewText: res.data.stories[0].content.description,
          thumbnailUrl: res.data.stories[0].content.images.filename,
          tags: res.data.stories[0].tag_list,
          github: res.data.stories[0].content.github.url,
          live: res.data.stories[0].content.live.url,
        };
      });
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/articles/_projects.scss";
</style>
