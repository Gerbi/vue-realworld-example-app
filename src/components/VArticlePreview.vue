<template>
  <div class="bg-background-secondary p-4 rounded-lg mb-4">
    <RwvArticleMeta isPreview :article="article" />
    <router-link :to="articleLink" class="text-copy-primary focus:outline-none">
      <h1 class="text-lg text-copy-primary" v-text="article.title" />
      <p v-text="article.description" class="text-sm text-copy-secondary" />
      <span class="text-blue-500">Read more...</span>
      <TagList :tags="article.tagList" />
    </router-link>
  </div>
</template>

<script>
import RwvArticleMeta from "./ArticleMeta";
import TagList from "./TagList";

export default {
  name: "RwvArticlePreview",
  components: {
    RwvArticleMeta,
    TagList
  },
  props: {
    article: { type: Object, required: true }
  },
  computed: {
    articleLink() {
      return {
        name: "article",
        params: {
          slug: this.article.slug
        }
      };
    }
  }
};
</script>
