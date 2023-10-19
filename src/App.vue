<template>
  <NavBar
    :nav-link-click="(index) => (activePage = index)"
    :pages="pages"
    :active-page="activePage"
  ></NavBar>
  <!-- <PageView v-if="pages.length > 0" :page="pages[activePage]" /> -->
  <create-page :page-created="pageCreated"></create-page>
</template>

<script>
import NavBar from "./components/NavBar.vue";
import PageView from "./components/PageView.vue";
import CreatePage from "./components/CreatePage.vue";

export default {
  components: {
    // eslint-disable-next-line vue/no-unused-components
    NavBar,
    // eslint-disable-next-line vue/no-unused-components
    PageView,
    CreatePage,
  },
  created() {
    this.getPages();
  },
  data() {
    return {
      activePage: 0,
      pages: [],
    };
  },
  methods: {
    async getPages() {
      // eslint-disable-next-line no-unused-vars
      let res = await fetch("pages.json");
      let data = await res.json();
      this.pages = data;
    },
    pageCreated(pageObject) {
      this.pages.push(pageObject);
    },
  },
};
</script>
