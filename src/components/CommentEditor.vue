<template>
  <div>
    <RwvListErrors :errors="errors" />
    <form class="card comment-form" @submit.prevent="onSubmit(slug, comment)">
      <div class="my-2">
        <textarea
          class="bg-gray-200 appearance-none border-2 border-border-color-primary rounded-md bg-background-primary w-full py-2 px-4 text-copy-primary leading-tight focus:outline-none focus:bg-background-primary focus:border-blue-500"
          v-model="comment"
          placeholder="Write a comment..."
          rows="2"
        >
        </textarea>
      </div>
      <div class="flex items-center justify-end my-4">
        <img :src="userImage" class="h-8 w-8 rounded-full object-cover mr-2" />
        <button
          class="btn btn-sm bg-blue-500 px-4 py-1 text-white rounded-lg focus:outline-none"
        >
          Post Comment
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import RwvListErrors from "./ListErrors.vue";
import { COMMENT_CREATE } from "../store/actions.type.js";

export default {
  name: "RwvCommentEditor",
  components: { RwvListErrors },
  props: {
    slug: { type: String, required: true },
    content: { type: String, required: false },
    userImage: { type: String, required: false }
  },
  data() {
    return {
      comment: this.content || null,
      errors: {}
    };
  },
  methods: {
    onSubmit(slug, comment) {
      this.$store
        .dispatch(COMMENT_CREATE, { slug, comment })
        .then(() => {
          this.comment = null;
          this.errors = {};
        })
        .catch(({ response }) => {
          this.errors = response.data.errors;
        });
    }
  }
};
</script>
