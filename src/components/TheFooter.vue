<template>
  <footer
    class="bg-background-secondary border-t border-border-color-primary shadow py-2"
  >
    <div class="flex justify-center text-center bg-background-secondary">
      <router-link class="text-blue-500" :to="{ name: 'home', params: {} }">
        Clone VK
      </router-link>
      <span class="ml-2 text-copy-primary">
        This is project clone on original repository
        <a
          rel="noopener noreferrer"
          class="text-blue-500"
          target="blank"
          href="https://github.com/gothinkster/vue-realworld-example-app"
          >Github</a
        >
      </span>
    </div>
  </footer>
</template>

<script>
export default {
  name: "RwvFooter"
};
</script>
