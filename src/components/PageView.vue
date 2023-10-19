<template>
  <main id="content" class="container">
    <h1>{{ page.pageTitle }}</h1>
    <p>{{ page.content }}</p>
  </main>
</template>

<script>
export default {
  props: ["page"],
};
</script>
