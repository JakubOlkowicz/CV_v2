<template>
  <article id="jobs" class="jobs">
    <div class="container pause">
      <h1 class="title">{{ title }}</h1>
      <p>
        {{ descript }}
      </p>

      <div class="skills-wrapper pause">
        <h2 class="title">Language and frameworks</h2>
        <div>
          <SkillList
            v-for="lang in languages"
            :key="lang.index"
            :img="lang.img"
          />
        </div>
        <h2 class="title">Tools</h2>
        <div>
          <SkillList v-for="tool in tools" :key="tool.index" :img="tool.img" />
        </div>
      </div>
      <div class="jobs-wrapper">
        <div class="work">
          <h2 class="title">experience</h2>
          <JobsList
            v-for="work in works"
            :key="work.id"
            :data="work.data"
            :place="work.place"
            :town="work.town"
            :doing="work.doing"
          />
        </div>
        <div class="school">
          <h2 class="title">School</h2>
          <JobsList
            v-for="school in schools"
            :key="school.id"
            :data="school.data"
            :place="school.place"
            :town="school.town"
            :doing="school.doing"
          />
        </div>
      </div>
    </div>
  </article>
</template>
<script>
import SkillList from "@/components/Jobs/SkillList.vue";
import JobsList from "@/components/Jobs/JobsList.vue";

export default {
  components: { SkillList, JobsList },
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "jobs/",
      })
      .then((res) => {
        return {
          languages: res.data.stories[0].content.lang.map((i) => {
            return {
              img: i.filename,
            };
          }),
          tools: res.data.stories[0].content.tool.map((t) => {
            return {
              img: t.filename,
            };
          }),
          works: res.data.stories[0].content.work.map((w) => {
            return {
              id: w.index,
              data: w.data,
              place: w.place,
              doing: w.doing,
              town: w.town,
            };
          }),
          schools: res.data.stories[0].content.school.map((s) => {
            return {
              id: s.index,
              data: s.data,
              place: s.town,
              doing: s.doing,
              town: s.town,
            };
          }),
        };
      });
  },
  data() {
    return {
      title: "my skills",
      descript:
        "I am not the best at everything, so knowing this, I try to develop every skill through hard work",
    };
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/articles/_jobs.scss";
</style>
