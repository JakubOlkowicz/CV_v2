<template>
  <main>
    <Menu />
    <Me />
    <Content />
  </main>
</template>
<script>
import Menu from "@/components/Menu.vue";
import Me from "@/components/Me.vue";
import Content from "@/components/Content.vue";

export default {
  components: {
    Menu,
    Me,
    Content,
  },
};
</script>
<style>
@import "@/assets/scss/_global.scss";
</style>
