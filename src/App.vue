<template>
  <div id="app">
    <form @submit.prevent="validateBeforeSubmit" v-if="!formSubmitted">
      <h1>Payment Information</h1>

      <div class="form-group" :class="{'has-error': errors.has('email') }">
        <label class="control-label" for="email">Email</label>
        <input
          v-model="email"
          v-validate.initial="email"
          data-rules="required|email"
          class="form-control"
          type="email"
          placeholder="Email"
        />
        <p class="text-danger" v-if="errors.has('email')">{{ errors.first('email') }}</p>
      </div>

      <div class="form-group" :class="{'has-error': errors.has('cardNumber') }">
        <label class="control-label" for="name">Card Information</label>
        <input
          v-model="cardNumber"
          v-validate.initial="cardNumber"
          data-rules="required|cardnumber"
          class="form-control"
          type="text"
          placeholder="1234 1234 1234 1234"
        />
        <p class="text-danger" v-if="errors.has('cvc')">{{ errors.first('cvc') }}</p>
      </div>

      <button class="btn btn-primary btn-block" type="submit">Submit</button>
    </form>
    <div v-else>
      <h1 class="submitted">Form submitted successfully!</h1>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import VeeValidate from "vee-validate";

Vue.use(VeeValidate);

VeeValidate.Validator.extend("passphrase", {
  getMessage: field => "Sorry dude, wrong pass phrase.",
  validate: value => value.toUpperCase() == "Demogorgon".toUpperCase()
});

export default {
  data() {
    return {
      email: "",
      name: "",
      url: "",
      secret: "",
      formSubmitted: false
    };
  },
  methods: {
    validateBeforeSubmit(e) {
      this.$validator.validateAll();

      if (!this.errors.any()) {
        this.submitForm();
      }
    },
    submitForm() {
      this.formSubmitted = true;
    }
  }
};
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
.container {
  width: 500px;
}
h1 {
  text-align: center;
}
img {
  text-align: center;
}
.submitted {
  color: #4fc08d;
}
</style>
