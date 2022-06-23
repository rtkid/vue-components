<template>
  <header class="header" ref="header">
    <nav-bar></nav-bar>
    <scroll-up></scroll-up>
  </header>
</template>

<script>
import NavBar from "@/components/NavBar/NavBar.vue";
import ScrollUp from "@/components/ScrollUp.vue";

export default {
  components: { NavBar, ScrollUp },

  mounted() {
    window.addEventListener("scroll", this.scrollHeader);
  },
  unmounted() {
    window.removeEventListener("scroll", this.scrollHeader);
  },

  methods: {
    scrollHeader() {
      if (window.scrollY >= 50)
        this.$refs.header.classList.add("scroll-header");
      else this.$refs.header.classList.remove("scroll-header");
    },
  },
};
</script>

<style scoped>
.scroll-header {
  background-color: var(--body-color);
}
</style>
