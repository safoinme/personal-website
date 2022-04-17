<template>
  <span>
    <ArticleCard
      v-for="article in articles"
      :key="article.slug"
      :article="article"
    ></ArticleCard>
  </span>
</template>

<script>
export default {
  layout: "blog-index",

  async asyncData({ $content, params }) {
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
