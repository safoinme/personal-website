<template>
  <v-row>
    <v-col cols="8">
      <article>
        <nuxt-content :document="article"></nuxt-content>
      </article>
    </v-col>

    <v-col cols="4">
      <p class="text-h5">Table of Contents</p>
      <TableOfContents :toc="article.toc" />
    </v-col>
  </v-row>
</template>

<script>
export default {
  layout: "article",
  async asyncData({ $content, params }) {
    const article = await $content("articles", params.slug).fetch();

    return { article };
  },
};
</script>
