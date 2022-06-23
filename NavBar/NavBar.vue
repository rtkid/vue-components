<template>
  <nav class="nav container">
    <a href="#" class="nav__logo">
      <img src="@/assets/img/logo.png" alt="" />
    </a>

    <div class="nav__menu" ref="navMenu">
      <ul class="nav__list">
        <li v-for="link in navLinks" :key="link.id" @click="toogleMenu()">
          <a :href="'#' + link.id" class="nav__link">{{ link.text }}</a>
        </li>
      </ul>

      <div class="nav__close" @click="toogleMenu()">
        <i class="ri-close-line"></i>
      </div>
    </div>

    <div class="nav__toggle" @click="toogleMenu()">
      <i class="ri-function-line"></i>
    </div>
  </nav>
</template>

<script>
export default {
  mounted() {
    window.addEventListener("scroll", this.scrollActive);
  },
  unmounted() {
    window.removeEventListener("scroll", this.scrollActive);
  },

  data() {
    return {
      isVisible: false,
      navLinks: [
        { id: "home", text: "Домой" },
        { id: "specs", text: "Характеристики" },
        { id: "case", text: "Кейс" },
        { id: "products", text: "Продукты" },
      ],
    };
  },

  methods: {
    toogleMenu() {
      this.$refs.navMenu.classList.toggle("show-menu");
    },

    scrollActive() {
      const scrollY = window.scrollY;

      this.navLinks.forEach((item) => {
        const section = document.getElementById(item.id);
        const sectionHeight = section.offsetHeight;
        const sectionTop = section.offsetTop - 50;

        const currentItem = document.querySelector(
          ".nav__menu a[href*=" + item.id + "]"
        );

        if (scrollY > sectionTop && scrollY <= sectionTop + sectionHeight) {
          currentItem.classList.add("active-link");
        } else {
          currentItem.classList.remove("active-link");
        }
      });
    },
  },
};
</script>

<style scoped>
.nav {
  height: var(--header-height);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav__logo {
  display: flex;
  width: 1.5rem;
}

.nav__toggle {
  font-size: 1.2rem;
  color: var(--white-color);
  cursor: pointer;
}

@media screen and (max-width: 767px) {
  .nav__menu {
    position: fixed;
    background-color: var(--body-color);
    top: -100%;
    left: 0;
    width: 100%;
    padding: 4rem 0 3rem;
    transition: 0.4s;
  }
}

.nav__list {
  display: flex;
  flex-direction: column;
  align-items: center;
  row-gap: 1rem;
}

.nav__close {
  position: absolute;
  font-size: 1.5rem;
  top: 1rem;
  right: 1rem;
  color: var(--white-color);
  cursor: pointer;
}

.nav__link {
  color: var(--white-color);
  font-size: var(--h2-font-size);
  text-transform: uppercase;
  font-weight: var(--font-semi-bold);
  background: var(--text-gradient);
  color: transparent;
  background-clip: text;
}

.nav__link:hover {
  background: var(--white-color);
  color: transparent;
  background-clip: text;
}

.active-link {
  background: var(--white-color);
  color: transparent;
  background-clip: text;
}

.show-menu {
  top: 0;
}

@media screen and (min-width: 767px) {
  .nav {
    height: calc(var(--header-height) + 1.5rem);
  }

  .nav__logo {
    width: 2rem;
  }

  .nav__list {
    flex-direction: row;
    column-gap: 3.5rem;
  }

  .nav__link {
    font-size: var(--normal-font-size);
    text-transform: initial;
  }

  .nav__toggle,
  .nav__close {
    display: none;
  }
}
</style>
