<template>
  <div class="container mb-3">
    <form action="">
      <div class="row">
        <div class="col-md-8">
          <div class="mb-3">
            <label for="" class="form-label"> Page Title </label>
            <input type="text" class="form-control" v-model="pageTitle" />
          </div>
          <div class="mb-3">
            <label for="" class="form-label"> Content </label>
            <textarea
              type="text"
              rows="5"
              class="form-control"
              v-model="content"
            ></textarea>
          </div>
        </div>
      </div>
      <div class="col">
        <div class="mb-3">
          <label for="" class="form-label">Link Text</label>
          <input type="text" class="form-control" v-model="linkText" />
        </div>
      </div>
      <div class="mb-3">
        <label for="" class="form-label">Link Url</label>
        <input type="text" class="form-control" v-model="linkUrl" />
      </div>
      <div class="row mb-3">
        <div class="form-check">
          <input type="checkbox" class="form-check-input" v-model="published" />
          <label for="gridCheck1" class="form-check-label">Published</label>
        </div>
      </div>
      <div class="mb-3">
        <button
          class="btn btn-primary"
          @click.prevent="submitForm"
          :disabled="isFormInvalid"
        >
          Create Page
        </button>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  emits: {
    // eslint-disable-next-line vue/return-in-emits-validator
    pageCreated({ pageTitle, content, link }) {
      if (!pageTitle || !content || !link.text || !link.url) {
        return false;
      }
      return true;
    },
  },
  props: ["pageCreated"],
  computed: {
    isFormInvalid() {
      return (
        !this.pageTitle || !this.content || !this.linkText || !this.linkUrl
      );
    },
  },
  data() {
    return {
      pageTitle: "",
      content: "",
      linkText: "",
      linkUrl: "",
      published: true,
    };
  },
  methods: {
    submitForm() {
      if (!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) {
        alert("Please fill out the form");
        return;
      }

      this.$emit("pageCreated", {
        pageTitle: this.pageTitle,
        content: this.content,
        link: {
          text: this.linkText,
          url: this.linkUrl,
        },
        published: this.published,
      });

      this.pageTitle = "";
      this.content = "";
      this.linkText = "";
      this.linkUrl = "";
      this.published = true;
    },
  },
  watch: {
    pageTitle(newTitle, oldTitle) {
      if (this.linkText == oldTitle) {
        this.linkText = newTitle;
      }
    },
  },
};
</script>
