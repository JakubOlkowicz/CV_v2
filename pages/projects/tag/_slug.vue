<template>
  <article class="projects view">
    <h1 class="title">#{{ tag_slug }}</h1>
    <div class="btns">
      <NuxtLink to="/projects" class="btn">back to all</NuxtLink>
    </div>

    <masonry
      :cols="{ default: 2, 400: 1 }"
      :gutter="{ default: '15px', 400: '10px' }"
      class="container"
    >
      <ProjectsPreview
        v-for="project in projects"
        :id="project.id"
        :key="`pro-${project.id}`"
        :slug="`/projects/${project.id}`"
        :title="project.title"
        :thumbnail-url="project.thumbnailUrl"
        :on-make="project.onMake"
      />
    </masonry>
  </article>
</template>

<script>
import ProjectsPreview from "@/components/Projects/ProjectsPreview.vue";
import kebabCase from "lodash/kebabCase";

export default {
  components: { ProjectsPreview },
  async asyncData({ app, params }) {
    const { data: tagsData } = await app.$storyapi.get("cdn/tags/");
    const topic = tagsData.tags.find((t) => kebabCase(t.name) === params.slug);
    // console.log(topic);
    return app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "projects/",
        with_tag: topic.name,
      })
      .then((res) => {
        // console.log(res.data.stories);
        return {
          projects: res.data.stories.map((bp) => {
            return {
              id: bp.slug,
              title: bp.content.title,
              previewText: bp.content.description,
              thumbnailUrl: bp.content.images.filename,
              onMake: bp.content.on_make,
              tags: bp.tag_list,
            };
          }),
          tag_slug: topic.name,
        };
      });
  },

  data() {
    return {
      title: "My Projects",
    };
  },

  methods: {
    tagSlug(tag) {
      return kebabCase(tag);
    },
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/articles/_projects.scss";
</style>
