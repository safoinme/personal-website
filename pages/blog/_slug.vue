<template>
  <span>
    <p class="mb-0 mt-10" id="title">{{ article.title }}</p>
    <span class="text-subtitle-2 font-weight-medium">
      {{ formatDate(article.createdAt) }} - 20 min read
    </span>
    <nuxt-content class="mt-5 text-h6" :document="article"></nuxt-content>
  </span>
</template>

<script>
export default {
  layout: "blog-index",
  async asyncData({ $content, params }) {
    const article = await $content("articles", params.slug).fetch();

    return { article };
  },
  methods: {
    formatDate(date) {
      const options = {
        year: "numeric",
        month: "long",
        day: "numeric",
      };
      return new Date(date).toLocaleDateString("en", options);
    },
  },
};
</script>
<style>
h1,
h2,
h3,
h4,
h5,
h6 {
  margin-bottom: 15px;
  margin-top: 20px;
}

#title {
  font-size: 2.7rem;
  font-weight: 900;
}
</style>
