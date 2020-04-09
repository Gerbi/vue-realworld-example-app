<template>
  <!-- eslint-disable max-len -->
  <div
    id="app"
    class="flex flex-col min-h-screen antialiased bg-background-primary"
    :class="theme"
  >
    <div class="sticky top-0 z-40 bg-background-primary md:pb-2">
      <div
        class="border-b shadow bg-background-secondary border-border-color-primary"
      >
        <div
          class="container max-w-screen-lg mx-auto md:px-6 lg:px-12 xl:px-18"
        >
          <div
            class="flex-wrap items-center justify-between hidden py-1 bg-background-secondary md:flex"
          >
            <div class="flex block w-1/4 mr-4">
              <router-link
                to="/"
                class="flex items-center text-xl font-semibold"
              >
                <svg
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  class="w-8 h-8 text-blue-600"
                >
                  <path
                    fill-rule="evenodd"
                    d="M18 13V5a2 2 0 00-2-2H4a2 2 0 00-2 2v8a2 2 0 002 2h3l3 3 3-3h3a2 2 0 002-2zM5 7a1 1 0 011-1h8a1 1 0 110 2H6a1 1 0 01-1-1zm1 3a1 1 0 100 2h3a1 1 0 100-2H6z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
              </router-link>
            </div>
            <div class="hidden mr-auto md:relative md:block">
              <div class="items-center justify-between py-2 md:flex">
                <span
                  class="flex items-center text-lg font-semibold text-copy-primary focus:outline-none"
                  v-if="!isAuthenticated"
                >
                  <p v-if="openTab === 0">Home</p>
                  <p v-if="openTab === 12">Sign In</p>
                  <p v-if="openTab === 13">Sign Up</p>
                  <svg
                    fill="currentColor"
                    viewBox="0 0 20 20"
                    class="w-5 h-5 ml-1 text-blue-600"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                      clip-rule="evenodd"
                    ></path>
                  </svg>
                </span>
                <span
                  v-else
                  class="flex items-center text-lg font-semibold text-copy-primary focus:outline-none"
                >
                  <p v-if="openTab === 0">Feed</p>
                  <p v-if="openTab === 1">{{ currentUser.username }}</p>
                  <p v-if="openTab === 2">Feed</p>
                  <p v-if="openTab === 3">New Post</p>
                  <svg
                    fill="currentColor"
                    viewBox="0 0 20 20"
                    class="w-5 h-5 ml-1 text-blue-600"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                      clip-rule="evenodd"
                    ></path>
                  </svg>
                </span>
              </div>
            </div>
            <Theme :theme="theme" @themeChanged="updateTheme" />
            <div
              class="items-center hidden xl:max-w-xs md:block md:flex md:relative"
            >
              <form>
                <div class="absolute inset-y-0 left-0 flex items-center pl-3">
                  <svg
                    class="w-5 h-5 text-gray-600 fill-current"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                    width="24"
                    height="24"
                  >
                    <path
                      d="M12.9 14.32a8 8 0 1 1 1.41-1.41l5.35 5.33-1.42 1.42-5.33-5.34zM8 14A6 6 0 1 0 8 2a6 6 0 0 0 0 12z"
                    />
                  </svg>
                </div>
                <input
                  @click="searchBar = true"
                  class="w-64 py-2 pl-10 pr-4 leading-none text-gray-900 border border-transparent rounded-lg bg-background-primary focus:outline-none focus:bg-background-primary focus:border-gray-300"
                  placeholder="Search"
                />
                <div
                  v-if="searchBar"
                  @click="searchBar = false"
                  class="fixed inset-0"
                  tabindex="-1"
                ></div>
                <transition
                  enter-class="scale-90 opacity-0"
                  enter-active-class="ease-out transition-fastest"
                  enter-to-class="scale-100 opacity-100"
                  leave-class="scale-100 opacity-100"
                  leave-active-class="ease-in transition-fastest"
                  leave-to-class="scale-90 opacity-0"
                >
                  <div
                    v-if="searchBar"
                    class="absolute mx-auto mt-4 text-left origin-top-right"
                  >
                    <div
                      class="w-64 h-56 py-1 overflow-y-auto border rounded-lg shadow-lg bg-background-secondary border-border-color-primary"
                    >
                      <div>
                        <a
                          href="#"
                          class="block px-4 py-2 leading-tight button-hover button-hover:hover"
                        >
                          <div class="flex items-center">
                            <img
                              src="https://images.unsplash.com/photo-1551292831-023188e78222?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1024&q=80"
                              alt=""
                              class="object-cover w-8 h-8 rounded-full"
                            />
                            <div class="ml-3">
                              <span
                                class="block text-sm font-medium leading-none text-copy-primary"
                                >Lisa M.</span
                              >
                              <span class="text-xs text-gray-600"
                                >lisa@example.test</span
                              >
                            </div>
                          </div>
                        </a>
                        <a
                          href="#"
                          class="block px-4 py-2 leading-tight button-hover button-hover:hover"
                        >
                          <div class="flex items-center">
                            <img
                              src="https://images.unsplash.com/photo-1551292831-023188e78222?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1024&q=80"
                              alt=""
                              class="object-cover w-8 h-8 rounded-full"
                            />
                            <div class="ml-3">
                              <span
                                class="block text-sm font-medium leading-none text-copy-primary"
                                >John Doe</span
                              >
                              <span class="text-xs text-gray-600"
                                >john@example.test</span
                              >
                            </div>
                          </div>
                        </a>
                      </div>
                    </div>
                  </div>
                </transition>
              </form>
            </div>
          </div>
        </div>
        <div class="flex justify-between px-4 py-1 shadow-sm md:hidden">
          <router-link to="/" class="flex items-center text-xl font-semibold">
            <svg
              fill="currentColor"
              viewBox="0 0 20 20"
              class="w-8 h-8 text-blue-600"
            >
              <path
                fill-rule="evenodd"
                d="M18 13V5a2 2 0 00-2-2H4a2 2 0 00-2 2v8a2 2 0 002 2h3l3 3 3-3h3a2 2 0 002-2zM5 7a1 1 0 011-1h8a1 1 0 110 2H6a1 1 0 01-1-1zm1 3a1 1 0 100 2h3a1 1 0 100-2H6z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </router-link>
          <button
            class="py-2 text-gray-500 hover:text-blue-600 focus:outline-none"
          >
            <svg viewBox="0 0 24 24" class="fill-current h-7 w-7">
              <path
                d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>
    <div
      class="container flex max-w-screen-lg mx-auto md:px-6 lg:px-12 xl:px-18 bg-background-primary"
    >
      <div class="hidden lg:block lg:w-1/4">
        <div class="fixed hidden w-48 mt-4 lg:block md:mt-0">
          <ul v-if="!isAuthenticated">
            <li>
              <router-link
                class="w-full"
                active-class="active"
                exact
                :to="{ name: 'home' }"
              >
                <div
                  class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                  v-on:click="toggleTabs(11)"
                  v-bind:class="{
                    'text-gray-600 bg-vkbody': openTab !== 11,
                    'text-gray-700 bg-background-senary': openTab === 11
                  }"
                >
                  <span class="inline-flex items-center">
                    <svg
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      class="w-6 h-6 text-blue-500"
                    >
                      <path
                        d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z"
                      ></path>
                    </svg>
                    <span class="ml-4 text-gray-800 text-copy-primary"
                      >Home</span
                    >
                  </span>
                </div>
              </router-link>
            </li>
            <li class="nav-item">
              <router-link
                class="nav-link"
                active-class="active"
                exact
                :to="{ name: 'login' }"
              >
                <div
                  class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                  v-on:click="toggleTabs(12)"
                  v-bind:class="{
                    'text-gray-600 bg-vkbody': openTab !== 12,
                    'text-gray-700 bg-background-senary': openTab === 12
                  }"
                >
                  <span class="inline-flex items-center">
                    <svg
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      class="w-6 h-6 text-blue-500"
                    >
                      <path
                        d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z"
                      ></path>
                      <path
                        fill-rule="evenodd"
                        d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <span class="ml-4 text-gray-800 text-copy-primary"
                      >Sign In</span
                    >
                  </span>
                </div>
              </router-link>
            </li>
            <li class="nav-item">
              <router-link
                class="nav-link"
                active-class="active"
                exact
                :to="{ name: 'register' }"
              >
                <div
                  class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                  v-on:click="toggleTabs(13)"
                  v-bind:class="{
                    'text-gray-600 bg-vkbody': openTab !== 13,
                    'text-gray-700 bg-background-senary': openTab === 13
                  }"
                >
                  <span class="inline-flex items-center">
                    <svg
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      class="w-6 h-6 text-blue-500"
                    >
                      <path
                        d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z"
                      ></path>
                      <path
                        fill-rule="evenodd"
                        d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <span class="ml-4 text-gray-800 text-copy-primary"
                      >Sign Up</span
                    >
                  </span>
                </div>
              </router-link>
            </li>
          </ul>
          <ul v-else>
            <li v-if="currentUser.username">
              <router-link
                active-class="active"
                exact
                :to="{
                  name: 'profile',
                  params: { username: currentUser.username }
                }"
              >
                <div
                  class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                  v-on:click="toggleTabs(1)"
                  v-bind:class="{
                    'text-gray-800 bg-vkbody': openTab !== 1,
                    'text-gray-800 bg-background-senary': openTab === 1
                  }"
                >
                  <span class="inline-flex items-center">
                    <img
                      src="https://images.unsplash.com/photo-1551292831-023188e78222?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1024&q=80"
                      alt=""
                      class="object-cover w-8 h-8 rounded-full"
                    />
                    <p class="ml-4 text-copy-primary">
                      {{ currentUser.username }}
                    </p>
                  </span>
                </div>
              </router-link>
            </li>
            <li>
              <router-link
                class="w-full"
                active-class="active"
                exact
                :to="{ name: 'home' }"
              >
                <div
                  class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                  v-on:click="toggleTabs(2)"
                  v-bind:class="{
                    'text-gray-600 bg-vkbody': openTab !== 2,
                    'text-gray-700 bg-background-senary': openTab === 2
                  }"
                >
                  <span class="inline-flex items-center">
                    <svg
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      class="w-6 h-6 text-blue-500"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M5 3a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2V5a2 2 0 00-2-2H5zm0 2h10v7h-2l-1 2H8l-1-2H5V5z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <span class="ml-4 text-gray-800 text-copy-primary"
                      >Feed</span
                    >
                  </span>
                </div>
              </router-link>
            </li>
            <li>
              <router-link
                class="w-full"
                active-class="active"
                :to="{ name: 'article-edit' }"
              >
                <div
                  class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                  v-on:click="toggleTabs(3)"
                  v-bind:class="{
                    'text-gray-600 bg-vkbody': openTab !== 3,
                    'text-gray-700 bg-background-senary': openTab === 3
                  }"
                >
                  <span class="inline-flex items-center">
                    <svg
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      class="w-6 h-6 text-blue-500"
                    >
                      <path
                        d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z"
                      ></path>
                      <path
                        fill-rule="evenodd"
                        d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <span class="ml-4 text-gray-800 text-copy-primary"
                      >New Post</span
                    >
                  </span>
                </div>
              </router-link>
            </li>
            <li>
              <div
                class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                v-on:click="toggleTabs(4)"
                v-bind:class="{
                  'text-gray-600 bg-vkbody': openTab !== 4,
                  'text-gray-700 bg-background-senary': openTab === 4
                }"
              >
                <span class="inline-flex items-center">
                  <svg
                    viewBox="0 0 24 24"
                    class="w-6 h-6 text-blue-500 fill-current"
                  >
                    <path
                      d="M12 12a5 5 0 1 1 0-10 5 5 0 0 1 0 10zm0-2a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm9 11a1 1 0 0 1-2 0v-2a3 3 0 0 0-3-3H8a3 3 0 0 0-3 3v2a1 1 0 0 1-2 0v-2a5 5 0 0 1 5-5h8a5 5 0 0 1 5 5v2z"
                    />
                  </svg>
                  <span class="ml-4 text-gray-800 text-copy-primary"
                    >Friends</span
                  >
                </span>
              </div>
            </li>
            <li>
              <router-link to="/">
                <div
                  class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                  v-on:click="toggleTabs(5)"
                  v-bind:class="{
                    'text-gray-600 bg-vkbody': openTab !== 5,
                    'text-gray-700 bg-background-senary': openTab === 5
                  }"
                >
                  <span class="inline-flex items-center">
                    <svg
                      viewBox="0 0 24 24"
                      class="w-6 h-6 text-blue-500 fill-current"
                    >
                      <path
                        d="M9 12A5 5 0 1 1 9 2a5 5 0 0 1 0 10zm0-2a3 3 0 1 0 0-6 3 3 0 0 0 0 6zm7 11a1 1 0 0 1-2 0v-2a3 3 0 0 0-3-3H7a3 3 0 0 0-3 3v2a1 1 0 0 1-2 0v-2a5 5 0 0 1 5-5h4a5 5 0 0 1 5 5v2zm1-5a1 1 0 0 1 0-2 5 5 0 0 1 5 5v2a1 1 0 0 1-2 0v-2a3 3 0 0 0-3-3zm-2-4a1 1 0 0 1 0-2 3 3 0 0 0 0-6 1 1 0 0 1 0-2 5 5 0 0 1 0 10z"
                      />
                    </svg>
                    <span class="ml-4 text-gray-800 text-copy-primary"
                      >Communities</span
                    >
                  </span>
                </div>
              </router-link>
            </li>
            <li>
              <router-link class="w-full" :to="{ name: 'settings' }">
                <div
                  class="flex items-center justify-between px-3 py-2 mt-1 -mx-3 text-sm font-medium rounded-lg focus:outline-none button-hover button-hover:hover"
                  v-on:click="toggleTabs(5)"
                  v-bind:class="{
                    'text-gray-600 bg-vkbody': openTab !== 5,
                    'text-gray-700 bg-background-senary': openTab === 5
                  }"
                >
                  <span class="inline-flex items-center">
                    <svg
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      class="w-6 h-6 text-blue-500"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M11.49 3.17c-.38-1.56-2.6-1.56-2.98 0a1.532 1.532 0 01-2.286.948c-1.372-.836-2.942.734-2.106 2.106.54.886.061 2.042-.947 2.287-1.561.379-1.561 2.6 0 2.978a1.532 1.532 0 01.947 2.287c-.836 1.372.734 2.942 2.106 2.106a1.532 1.532 0 012.287.947c.379 1.561 2.6 1.561 2.978 0a1.533 1.533 0 012.287-.947c1.372.836 2.942-.734 2.106-2.106a1.533 1.533 0 01.947-2.287c1.561-.379 1.561-2.6 0-2.978a1.532 1.532 0 01-.947-2.287c.836-1.372-.734-2.942-2.106-2.106a1.532 1.532 0 01-2.287-.947zM10 13a3 3 0 100-6 3 3 0 000 6z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <span class="ml-4 text-gray-800 text-copy-primary"
                      >Settings</span
                    >
                  </span>
                </div>
              </router-link>
            </li>
          </ul>
        </div>
      </div>
      <div class="w-full mx-auto md:w-3/4 xl:pl-4">
        <router-view></router-view>
      </div>
    </div>
    <div class="fixed bottom-0 z-40 w-full mx-auto bg-background-primary">
      <RwvFooter />
    </div>
  </div>
</template>

<script>
import Theme from "./components/Theme.vue";
import RwvHeader from "@/components/TheHeader";
import RwvFooter from "@/components/TheFooter";
import { mapGetters } from "vuex";

export default {
  name: "App",
  components: {
    RwvHeader,
    RwvFooter,
    Theme
  },
  data() {
    return {
      theme: "",
      openTab: 0,
      searchBar: false
    };
  },
  computed: {
    ...mapGetters(["currentUser", "isAuthenticated"])
  },
  mounted() {
    this.theme = localStorage.getItem("theme") || "theme-light";
  },
  methods: {
    updateTheme(theme) {
      this.theme = theme;
    },
    toggleTabs(tabNumber) {
      this.openTab = tabNumber;
    }
  }
};
</script>

<style src="./assets/css/Tailwind.css"></style>
