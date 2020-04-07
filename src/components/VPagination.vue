<template>
  <nav>
    <ul class="hidden sm:flex sm:flex-wrap sm:items-center sm:justify-start">
      <li
        class="relative inline-flex items-center px-2 py-2 rounded-md border border-gray-300 bg-background-secondary text-sm leading-5 font-medium text-gray-500 hover:text-gray-400 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150"
        v-for="page in pages"
        :data-test="`page-link-${page}`"
        :key="page"
        :class="paginationClass(page)"
        @click.prevent="changePage(page)"
      >
        <a class="text-blue-500" href v-text="page" />
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "Pagination",
  props: {
    pages: {
      type: Array,
      required: true
    },
    currentPage: {
      type: Number,
      required: true
    }
  },
  methods: {
    changePage(goToPage) {
      if (goToPage === this.currentPage) return;
      this.$emit("update:currentPage", goToPage);
    },
    paginationClass(page) {
      return {
        "page-item": true,
        active: this.currentPage === page
      };
    }
  }
};
</script>
