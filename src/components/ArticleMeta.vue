<template>
  <div class="article-meta">
    <div class="flex justify-between items-center">
      <div class="flex">
        <router-link
          class="mr-3 bg-gray-500 rounded-full"
          :to="{
            name: 'profile',
            params: { username: article.author.username }
          }"
        >
          <img
            class="object-cover w-12 h-12 rounded-full"
            :src="article.author.image"
          />
        </router-link>
        <div class="flex">
          <div class="flex flex-col">
            <router-link
              :to="{
                name: 'profile',
                params: { username: article.author.username }
              }"
              class="text-copy-primary"
            >
              {{ article.author.username }}
            </router-link>
            <span class="text-gray-500 text-sm">{{
              article.createdAt | date
            }}</span>
          </div>
        </div>
      </div>
      <rwv-article-actions
        v-if="actions"
        :article="article"
        :canModify="isCurrentUser()"
      ></rwv-article-actions>
      <button
        v-else
        class="flex items-center items-center focus:outline-none"
        @click="toggleFavorite"
        :class="{
          'text-blue-500': article.favorited,
          'text-green-600': !article.favorited
        }"
      >
        <svg fill="currentColor" viewBox="0 0 20 20" class="w-4 h-4">
          <path
            fill-rule="evenodd"
            d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z"
            clip-rule="evenodd"
          ></path>
        </svg>
        <span class="text-copy-secondary ml-2">
          {{ article.favoritesCount }}
        </span>
      </button>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import RwvArticleActions from "@/components/ArticleActions";
import { FAVORITE_ADD, FAVORITE_REMOVE } from "@/store/actions.type";

export default {
  name: "RwvArticleMeta",
  components: {
    RwvArticleActions
  },
  props: {
    article: {
      type: Object,
      required: true
    },
    actions: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  computed: {
    ...mapGetters(["currentUser", "isAuthenticated"])
  },
  methods: {
    isCurrentUser() {
      if (this.currentUser.username && this.article.author.username) {
        return this.currentUser.username === this.article.author.username;
      }
      return false;
    },
    toggleFavorite() {
      if (!this.isAuthenticated) {
        this.$router.push({ name: "login" });
        return;
      }
      const action = this.article.favorited ? FAVORITE_REMOVE : FAVORITE_ADD;
      this.$store.dispatch(action, this.article.slug);
    }
  }
};
</script>
