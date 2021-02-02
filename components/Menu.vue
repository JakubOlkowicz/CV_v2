<template>
  <menu>
    <div class="navigation">
      <nuxt-link to="/" class="nav">
        <font-awesome-icon icon="user" />
      </nuxt-link>
      <nuxt-link to="/jobs" class="nav">
        <font-awesome-icon icon="user-graduate" />
      </nuxt-link>
      <nuxt-link to="/projects" class="nav">
        <font-awesome-icon icon="briefcase" />
      </nuxt-link>
      <nuxt-link to="/contact" class="nav">
        <font-awesome-icon icon="phone" />
      </nuxt-link>
      <div>
        <span> .pdf </span>
        <a :href="pdf" download="Olkowicz_CV" class="nav">
          <font-awesome-icon icon="cloud-download-alt" />
        </a>
      </div>
    </div>
  </menu>
</template>
<script>
import pdf from "../assets/images/Olkowicz_CV.pdf";
export default {
  name: "Menu",
  data() {
    return {
      pdf,
    };
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/sections/_menu.scss";
</style>
