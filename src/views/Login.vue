<template>
  <div class="p-4 mb-10 rounded-lg bg-background-secondary">
    <div class="container page">
      <div class="row">
        <div>
          <h1 class="mb-2 text-2xl font-semibold text-center text-copy-primary">
            Sign in
          </h1>
          <p class="mb-4 text-center text-blue-500">
            <router-link :to="{ name: 'register' }">
              Need an account?
            </router-link>
          </p>
          <ul v-if="errors" class="error-messages">
            <li v-for="(v, k) in errors" :key="k">{{ k }} {{ v | error }}</li>
          </ul>
          <form @submit.prevent="onSubmit(email, password)">
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
            <div class="flex justify-end">
              <button class="px-4 py-1 text-white bg-blue-500 rounded-lg">
                Sign in
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
import { LOGIN } from "@/store/actions.type";

export default {
  name: "RwvLogin",
  data() {
    return {
      email: null,
      password: null
    };
  },
  methods: {
    onSubmit(email, password) {
      this.$store
        .dispatch(LOGIN, { email, password })
        .then(() => this.$router.push({ name: "home" }));
    }
  },
  computed: {
    ...mapState({
      errors: state => state.auth.errors
    })
  }
};
</script>
