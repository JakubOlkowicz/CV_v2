<template>
  <article id="contact">
    <div class="container">
      <h1 class="title">Contact</h1>
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
      <div>
        <h2 class="title">send message</h2>
        <p v-if="errors.length" >
          <b>Please correct the following error(s):</b>
          <ul>
            <li v-for="error in errors" :key="`error-${error}`">
              {{error}}
            </li>
          </ul>
        </p>
        <form
          name="contact"
          action="/thank-you"
          netlify-honeypot="bot-field"
          method="post"
          netlify
          @submit="checkForm"
        >
          <input type="hidden" name="form-name" value="contact" />
          <p class="hidden">
            <label>Don’t fill this out: <input name="bot-field" /></label>
          </p>
          <div>
            <input
              id="name"
              v-model="name"
              class="form-field"
              name="name"
              placeholder="name"
            />
          </div>
          <div>
            <input
              id="email"
              v-model="email"
              class="form-field"
              name="email"
              placeholder="email"
            />
          </div>
          <div>
            <textarea
              id="message"
              v-model="message"
              class="form-field"
              name="message"
              placeholder="message"
            ></textarea>
          </div>
          <input class="btn" type="submit" value="Send message" onSubmit />
        </form>
      </div>
    </div>
  </article>
</template>
<script>
export default {
  data() {
    return {
      errors: [],
      name: null,
      email: null,
      message:null,
      hidden: null,
      discript:
        "If you are interested in my skills and services I invite you to contact me by phone, e-mail or contact form below",
      myPhone: "506-351-044",
      myEmail: "jakubaolkowicz@gmail.com",
    };
  },
  methods:{
    showErrorField: function(name){
      let input = document.querySelector(`[name="${name}"]`);
      input.style.borderColor = "red";
      console.log(input, name)
    },
    emailIsValid: function(email) {
      return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
    },
    checkForm: function (e) {
      if (this.name && this.email && this.message && !this.hidden) {
        if(!this.emailIsValid(this.email)){
          this.errors.push('Check correct your email');
          this.showErrorField("emial");

          e.preventDefault();
        }
        return true;
      }

      this.errors = [];

      if (!this.name) {
        this.errors.push('Name required.');
        this.showErrorField("name");
      }
      if (!this.email) {
        this.errors.push('Email required.');
        this.showErrorField("emial");

      }
      if (!this.message) {
        this.errors.push('Message required.');
        this.showErrorField("message");

      }
      if(this.hidden) {
        return false
      }
      e.preventDefault();
    }
}
}
</script>
<style lang="scss">
@import "@/assets/scss/articles/contact.scss";
</style>
