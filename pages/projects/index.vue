<template>
  <article class="projects">
    <h1 class="title">{{ title }}</h1>
    <div class="pause">
      <p>{{ discript }}</p>
    </div>
    <div class="btns">
      <nuxt-link
        v-for="tags in tagsData.tags"
        :key="`tag-${tags.name}`"
        :to="`/projects/tag/${tagSlug(tags.name)}`"
        class="btn"
        >{{ tags.name }}</nuxt-link
      >
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
        :excerpt="project.previewText"
        :thumbnail-url="project.thumbnailUrl"
        :on-make="project.onMake"
      />
    </masonry>
  </article>
</template>

<script>
import ProjectsPreview from "../../components/Projects/ProjectsPreview.vue";
import kebabCase from "lodash/kebabCase";

export default {
  name: "Projects",

  components: { ProjectsPreview },
  async asyncData({ app }) {
    const { data: tagsData } = await app.$storyapi.get("cdn/tags/");
    // console.log(tagsData);
    return app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "projects/",
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
          tagsData,
        };
      });
  },

  data() {
    return {
      title: "My Projects",
      discript:
        "Each project is treated individually, I try to comprehensively solve the problem of the client. I love to develop new skills, the bigger the problem for me the greater the joy of solving it",
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
