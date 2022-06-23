<template>
  <a href="#" class="scrollup" ref="scrollUp">
    <i class="ri-arrow-up-s-line scroll__icon"></i>
  </a>
</template>

<script>
export default {
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },

  unmounted() {
    window.removeEventListener("scroll", this.handleScroll);
  },

  methods: {
    handleScroll() {
      if (window.scrollY >= 200)
        this.$refs.scrollUp.classList.add("show-scroll");
      else this.$refs.scrollUp.classList.remove("show-scroll");
    },
  },
};
</script>

<style scoped>
.scrollup {
  position: fixed;
  right: 1rem;
  bottom: -20%;
  display: flex;
  background-color: var(--container-color);
  border-radius: 0.25rem;
  padding: 0.45rem;
  opacity: 9;
  z-index: var(--z-tooltip);
  transition: 0.4s;
}

.scrollup:hover {
  background-color: var(--first-color);
  opacity: 1;
  transform: translateY(-0.25rem);
}

.scroll__icon {
  color: var(--white-color);
  font-size: 1.35rem;
}

.show-scroll {
  bottom: 3rem;
}

@media screen and (min-width: 1040px) {
  .scrollup {
    right: 3rem;
  }
}
</style>
