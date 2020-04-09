<template>
  <div class="p-4 sm:rounded-lg bg-background-secondary mb-10">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="mb-2 text-2xl font-semibold text-center text-copy-primary">
            Sign up
          </h1>
          <p class="mb-4 text-center text-blue-500">
            <router-link :to="{ name: 'login' }">
              Have an account?
            </router-link>
          </p>
          <ul v-if="errors" class="error-messages">
            <li v-for="(v, k) in errors" :key="k">{{ k }} {{ v | error }}</li>
          </ul>
          <form @submit.prevent="onSubmit">
            <fieldset class="mb-4">
              <input
                class="w-full px-4 py-2 leading-tight bg-gray-200 border-2 rounded-md appearance-none border-border-color-primary bg-background-primary text-copy-secondary focus:outline-none focus:bg-background-primary focus:border-blue-500"
                type="text"
                v-model="username"
                placeholder="Username"
              />
            </fieldset>
            <fieldset class="mb-4">
              <input
                class="w-full px-4 py-2 leading-tight bg-gray-200 border-2 rounded-md appearance-none border-border-color-primary bg-background-primary text-copy-secondary focus:outline-none focus:bg-background-primary focus:border-blue-500"
                type="text"
                v-model="email"
                placeholder="Email"
              />
            </fieldset>
            <fieldset class="mb-4">
              <input
                class="w-full px-4 py-2 leading-tight bg-gray-200 border-2 rounded-md appearance-none border-border-color-primary bg-background-primary text-copy-secondary focus:outline-none focus:bg-background-primary focus:border-blue-500"
                type="password"
                v-model="password"
                placeholder="Password"
              />
            </fieldset>
            <div class="flex items-center justify-end">
              <button
                class="px-4 py-2 leading-none text-white bg-blue-500 rounded-lg"
              >
                Sign Up
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import { REGISTER } from "@/store/actions.type";

export default {
  name: "RwvRegister",
  data() {
    return {
      username: "",
      email: "",
      password: ""
    };
  },
  computed: {
    ...mapState({
      errors: state => state.auth.errors
    })
  },
  methods: {
    onSubmit() {
      this.$store
        .dispatch(REGISTER, {
          email: this.email,
          password: this.password,
          username: this.username
        })
        .then(() => this.$router.push({ name: "home" }));
    }
  }
};
</script>
