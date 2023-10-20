<template>
  <nav
    :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
  >
    <div class="container-fluid">
      <a href="#" class="navbar-brand">ToDoVue</a>
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li
          v-for="(page, index) in publishedPages"
          class="nav-item"
          :key="index"
        >
          <NavBarLink
            :page="page"
            :isActive="activePage == index"
            @click.prevent="navLinkClick(index)"
          ></NavBarLink>
        </li>
      </ul>
      <form action="" class="d-flex">
        <button class="btn btn-primary" @click.prevent="changeTheme">
          Toggle
        </button>
      </form>
    </div>
  </nav>
</template>

<script>
import NavBarLink from "./NavBarLink.vue";

export default {
  components: {
    NavBarLink,
  },
  computed: {
    publishedPages() {
      return this.pages.filter((p) => p.published);
    },
  },
  props: ["pages", "activePage", "navLinkClick"],
  data() {
    return {
      theme: "light",
    };
  },
  methods: {
    changeTheme() {
      let theme = "light";
      if (this.theme == "light") {
        theme = "dark";
      }
      this.theme = theme;
      this.storeThemeSetting();
    },
    storeThemeSetting() {
      localStorage.setItem("theme", this.theme);
    },
    getThemeSetting() {
      let theme = localStorage.getItem("theme", this.theme);

      if (theme) {
        this.theme = theme;
      }
    },
  },
};
</script>

<style scoped>
.emphasize {
  text-decoration: underline;
}
</style>
