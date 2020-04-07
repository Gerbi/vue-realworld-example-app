<template>
  <div class="bg-background-secondary p-4 rounded-lg">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="mb-2 text-md text-copy-primary font-semibold">
            Your Settings
          </h1>
          <form @submit.prevent="updateSettings()">
            <fieldset>
              <fieldset class="mb-4">
                <input
                  class="bg-gray-200 appearance-none border-2 border-border-color-primary rounded-md bg-background-primary w-full py-2 px-4 text-copy-secondary leading-tight focus:outline-none focus:bg-background-primary focus:border-blue-500"
                  type="text"
                  v-model="currentUser.image"
                  placeholder="URL of profile picture"
                />
              </fieldset>
              <fieldset class="mb-2">
                <input
                  class="bg-gray-200 appearance-none border-2 border-border-color-primary rounded-md bg-background-primary w-full py-2 px-4 text-copy-secondary leading-tight focus:outline-none focus:bg-background-primary focus:border-blue-500"
                  type="text"
                  v-model="currentUser.username"
                  placeholder="Your username"
                />
              </fieldset>
              <fieldset class="mb-2">
                <textarea
                  class="bg-gray-200 appearance-none border-2 border-border-color-primary rounded-md bg-background-primary w-full py-2 px-4 text-copy-secondary leading-tight focus:outline-none focus:bg-background-primary focus:border-blue-500"
                  rows="8"
                  v-model="currentUser.bio"
                  placeholder="Short bio about you"
                ></textarea>
              </fieldset>
              <fieldset class="mb-2">
                <input
                  class="bg-gray-200 appearance-none border-2 border-border-color-primary rounded-md bg-background-primary w-full py-2 px-4 text-copy-secondary leading-tight focus:outline-none focus:bg-background-primary focus:border-blue-500"
                  type="text"
                  v-model="currentUser.email"
                  placeholder="Email"
                />
              </fieldset>
              <fieldset class="mb-2">
                <input
                  class="bg-gray-200 appearance-none border-2 border-border-color-primary rounded-md bg-background-primary w-full py-2 px-4 text-copy-secondary leading-tight focus:outline-none focus:bg-background-primary focus:border-blue-500"
                  type="password"
                  v-model="currentUser.password"
                  placeholder="Password"
                />
              </fieldset>
              <button
                class="bg-blue-500 text-white px-4 rounded-lg py-1 text-md right-0"
              >
                Update Settings
              </button>
            </fieldset>
          </form>
          <!-- Line break for logout button -->
          <hr class="my-3 border border-border-color-primary" />
          <button
            @click="logout"
            class="bg-red-500 px-4 py-1 text-white rounded-lg"
          >
            Or click here to logout.
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import { LOGOUT, UPDATE_USER } from "@/store/actions.type";

export default {
  name: "RwvSettings",
  computed: {
    ...mapGetters(["currentUser"])
  },
  methods: {
    updateSettings() {
      this.$store.dispatch(UPDATE_USER, this.currentUser).then(() => {
        // #todo, nice toast and no redirect
        this.$router.push({ name: "home" });
      });
    },
    logout() {
      this.$store.dispatch(LOGOUT).then(() => {
        this.$router.push({ name: "home" });
      });
    }
  }
};
</script>
