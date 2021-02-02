<template>
  <article id="me" class="about">
    <div class="container">
      <h1 class="title">{{ me }}</h1>
      <div class="text-about pause">
        <h2>{{ title }}</h2>
        <p>{{ about }}</p>
      </div>
      <h2 class="title">
        {{ services }}
      </h2>
      <div class="skill-wrapper">
        <div
          v-for="(row, index) in technology"
          :key="`row-${index}`"
          class="skill"
        >
          <font-awesome-icon :icon="row.icon" />
          <span class="skill-title">{{ row.title }}</span>
          <p>{{ row.tech }}</p>
        </div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  name: "Home",
  components: {},
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories/home", {
        version: "draft",
      })
      .then((res) => {
        return res.data.story.content;
      })
      .catch((res) => {
        if (!res.response) {
          context.error({
            statusCode: 404,
            message: "Failed to receive content form api",
          });
        } else {
          context.error({
            statusCode: res.response.status,
            message: res.response.data,
          });
        }
      });
  },
  data() {
    return {
      story: {
        content: {},
      },
      me: "About Me",
      services: "My Services",
    };
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/articles/_home.scss";
</style>
