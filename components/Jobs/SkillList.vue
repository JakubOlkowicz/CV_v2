<template class="">
  <img :src="img" alt="" class="img-skill" />
</template>
<script>
export default {
  name: "SkillList",
  props: {
    img: {
      type: String,
      required: true,
    },
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/articles/_jobs.scss";
</style>
