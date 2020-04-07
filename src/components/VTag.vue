<template>
  <div class="flex">
    <router-link :to="homeRoute" :class="className" v-text="name"></router-link>
  </div>
</template>

<script>
export default {
  name: "RwvTag",
  props: {
    name: {
      type: String,
      required: true
    },
    className: {
      type: String,
      default: "text-blue-500 mx-2"
    }
  },
  computed: {
    homeRoute: () => ({ name: "home-tag", params: { tag: name } })
  }
};
</script>
