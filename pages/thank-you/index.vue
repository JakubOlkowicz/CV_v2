<template>
  <article id="contact">
    <div class="container">
      <h1 class="title">{{ title }}</h1>
      <div class="pause">
        <p>
          {{ discript }}
        </p>
        <div class="contact-single">
          <span>
            <font-awesome-icon icon="phone" />
            <p>{{ myPhone }}</p>
          </span>
          <span>
            <font-awesome-icon icon="envelope" />
            <p>{{ myEmail }}</p>
          </span>
        </div>
      </div>
      <nuxt-link to="/" class="btn">Back to Home</nuxt-link>
    </div>
  </article>
</template>
<script>
export default {
  data() {
    return {
      title: "Thank You <3",
      myPhone: "506-351-044",
      myEmail: "jakubaolkowicz@gmail.com",
      discript: "lorem ipsum",
    };
  },
};
</script>
<style lang="scss">
@import "@/assets/scss/articles/contact.scss";
</style>
