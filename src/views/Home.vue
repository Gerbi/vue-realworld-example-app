<template>
  <!-- eslint-disable max-len -->
  <div class="pb-5">
    <div class="home-page">
      <div class="container page">
        <div class="row">
          <div class="col-md-9">
            <div
              class="px-4 bg-background-secondary md:rounded-t-lg shadow-sm -mb-2"
            >
              <ul class="flex">
                <li v-if="isAuthenticated" class="flex mr-8 -mb-px">
                  <router-link
                    :to="{ name: 'home-my-feed' }"
                    class="flex items-center py-3 text-copy-secondary no-underline border-b-2 border-transparent opacity-50 md:opacity-100 hover:opacity-100 md:hover:border-gray-700"
                    active-class="border-blue-500"
                  >
                    Your Feed
                  </router-link>
                </li>
                <li class="flex mr-8 -mb-px">
                  <router-link
                    :to="{ name: 'home' }"
                    exact
                    class="flex items-center py-3 text-copy-secondary no-underline border-b-2 border-transparent opacity-50 md:opacity-100 hover:opacity-100 md:hover:border-gray-700"
                    active-class="border-blue-500"
                  >
                    Global Feed
                  </router-link>
                </li>
                <li class="nav-item" v-if="tag">
                  <router-link
                    :to="{ name: 'home-tag', params: { tag } }"
                    class="nav-link"
                    active-class="active"
                  >
                    <i class="ion-pound"></i> {{ tag }}
                  </router-link>
                </li>
              </ul>
            </div>
            <router-view></router-view>
          </div>
          <div class="bg-background-secondary rounded-lg p-4 mb-10">
            <div class="sidebar">
              <p class="text-copy-primary">Popular Tags</p>
              <div class="flex flex-wrap">
                <RwvTag v-for="(tag, index) in tags" :name="tag" :key="index">
                </RwvTag>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import RwvTag from "@/components/VTag";
import { FETCH_TAGS } from "@/store/actions.type";

export default {
  name: "home",
  components: {
    RwvTag
  },
  mounted() {
    this.$store.dispatch(FETCH_TAGS);
  },
  computed: {
    ...mapGetters(["isAuthenticated", "tags"]),
    tag() {
      return this.$route.params.tag;
    }
  }
};
</script>
