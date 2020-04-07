<template v-show="errors">
  <ul class="text-red-500 text-sm">
    <li v-for="(value, key) in errors" :key="key">
      <span v-text="key" />
      <span v-for="err in value" :key="err" v-text="err" />
    </li>
  </ul>
</template>

<script>
export default {
  name: "RwvListErorrs",
  props: {
    errors: { type: Object, required: true }
  }
};
</script>
