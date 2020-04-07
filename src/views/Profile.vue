<template>
  <div class="profile-page">
    <div class="user-info">
      <div class="container">
        <div class="row">
          <div class="bg-background-secondary rounded-lg">
            <div class="p-4">
              <img
                :src="profile.image"
                class="rounded-lg object-cover text-center"
              />
              <h4
                class="text-copy-primary text-center text-lg font-semibold my-2"
              >
                {{ profile.username }}
              </h4>
              <p>{{ profile.bio }}</p>
            </div>
            <div v-if="isCurrentUser()" class="px-4 pb-4">
              <router-link
                class="block w-full px-4 py-2 pl-10 flex items-center justify-center text-sm font-medium text-center text-copy-secondary bg-background-senary rounded-lg focus:outline-none focus:bg-gray-200"
                :to="{ name: 'settings' }"
              >
                <svg
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  class="w-7 h-7 text-copy-primary"
                >
                  <path
                    fill-rule="evenodd"
                    d="M11.49 3.17c-.38-1.56-2.6-1.56-2.98 0a1.532 1.532 0 01-2.286.948c-1.372-.836-2.942.734-2.106 2.106.54.886.061 2.042-.947 2.287-1.561.379-1.561 2.6 0 2.978a1.532 1.532 0 01.947 2.287c-.836 1.372.734 2.942 2.106 2.106a1.532 1.532 0 012.287.947c.379 1.561 2.6 1.561 2.978 0a1.533 1.533 0 012.287-.947c1.372.836 2.942-.734 2.106-2.106a1.533 1.533 0 01.947-2.287c1.561-.379 1.561-2.6 0-2.978a1.532 1.532 0 01-.947-2.287c.836-1.372-.734-2.942-2.106-2.106a1.532 1.532 0 01-2.287-.947zM10 13a3 3 0 100-6 3 3 0 000 6z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
                Edit Profile
              </router-link>
            </div>
            <div v-else class="flex">
              <button
                class="btn btn-sm btn-secondary action-btn"
                v-if="profile.following"
                @click.prevent="unfollow()"
              >
                <i class="ion-plus-round"></i> &nbsp;Unfollow
                {{ profile.username }}
              </button>
              <button
                class="btn btn-sm btn-outline-secondary action-btn"
                v-if="!profile.following"
                @click.prevent="follow()"
              >
                <i class="ion-plus-round"></i> &nbsp;Follow
                {{ profile.username }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <div class="col-xs-12 col-md-10 offset-md-1">
          <div
            class="px-4 mt-3 bg-background-secondary md:rounded-t-lg shadow-sm -mb-2"
          >
            <ul class="flex">
              <li class="flex mr-8 -mb-px">
                <router-link
                  class="flex items-center py-3 text-copy-secondary no-underline border-b-2 border-transparent opacity-50 md:opacity-100 hover:opacity-100 md:hover:border-gray-700"
                  active-class="border-blue-500"
                  exact
                  :to="{ name: 'profile' }"
                >
                  My Articles
                </router-link>
              </li>
              <li class="flex mr-8 -mb-px">
                <router-link
                  class="flex items-center py-3 text-copy-secondary no-underline border-b-2 border-transparent opacity-50 md:opacity-100 hover:opacity-100 md:hover:border-gray-700"
                  active-class="border-blue-500"
                  exact
                  :to="{ name: 'profile-favorites' }"
                >
                  Favorited Articles
                </router-link>
              </li>
            </ul>
          </div>
          <router-view></router-view>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import {
  FETCH_PROFILE,
  FETCH_PROFILE_FOLLOW,
  FETCH_PROFILE_UNFOLLOW
} from "@/store/actions.type";

export default {
  name: "RwvProfile",
  mounted() {
    this.$store.dispatch(FETCH_PROFILE, this.$route.params);
  },
  computed: {
    ...mapGetters(["currentUser", "profile", "isAuthenticated"])
  },
  methods: {
    isCurrentUser() {
      if (this.currentUser.username && this.profile.username) {
        return this.currentUser.username === this.profile.username;
      }
      return false;
    },
    follow() {
      if (!this.isAuthenticated) return;
      this.$store.dispatch(FETCH_PROFILE_FOLLOW, this.$route.params);
    },
    unfollow() {
      this.$store.dispatch(FETCH_PROFILE_UNFOLLOW, this.$route.params);
    }
  },
  watch: {
    $route(to) {
      this.$store.dispatch(FETCH_PROFILE, to.params);
    }
  }
};
</script>
