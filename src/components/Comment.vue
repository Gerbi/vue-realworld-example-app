<template>
  <div class="border-b border-border-color-primary py-2">
    <div class="flex items-center">
      <a href="" class="comment-author">
        <img
          :src="comment.author.image"
          class="rounded-full h-7 w-7 object-cover"
        />
      </a>
      <div class="flex flex-col ml-2">
        <router-link
          class="text-sm text-blue-500 font-medium leading-none"
          :to="{
            name: 'profile',
            params: { username: comment.author.username }
          }"
        >
          {{ comment.author.username }}
        </router-link>
        <span class="text-xs text-gray-600 leading-none">{{
          comment.createdAt | date
        }}</span>
        <span v-if="isCurrentUser" class="mod-options">
          <i class="ion-trash-a" @click="destroy(slug, comment.id)"></i>
        </span>
      </div>
    </div>
    <div class="card-block">
      <p class="text-copy-primary font-normal text-sm">{{ comment.body }}</p>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import { COMMENT_DESTROY } from "@/store/actions.type";

export default {
  name: "RwvComment",
  props: {
    slug: { type: String, required: true },
    comment: { type: Object, required: true }
  },
  computed: {
    isCurrentUser() {
      if (this.currentUser.username && this.comment.author.username) {
        return this.comment.author.username === this.currentUser.username;
      }
      return false;
    },
    ...mapGetters(["currentUser"])
  },
  methods: {
    destroy(slug, commentId) {
      this.$store.dispatch(COMMENT_DESTROY, { slug, commentId });
    }
  }
};
</script>
