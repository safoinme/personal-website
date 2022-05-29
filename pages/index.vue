<template>
  <span>
    <Header class="mb-10" />
    <ArticleCard
      v-for="article in articles"
      :key="article.slug"
      :article="article"
      class="mb-5"
    ></ArticleCard>
  </span>
</template>

<script>
export default {
  layout: "blog-index",

  async asyncData({ $content }) {
    const articles = await $content("articles")
      .only(["title", "description", "createdAt", "img", "slug", "author"])
      .sortBy("createdAt", "desc")
      .fetch();

    return {
      articles,
    };
  },
};
</script>
