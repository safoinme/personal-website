<template>
  <v-card :to="`/blog/` + article.slug" flat class="pa-5">
    <p class="text-h5 font-weight-black mb-2">
      {{ article.title }}
    </p>

    <div class="mb-5 font-weight-medium">
      {{ article.description }}...
    </div>

    <span class="mb-2 text-subtitle-2 font-weight-medium">
      {{ formatDate(article.createdAt) }} - 20 min read
    </span>
  </v-card>
</template>

<script>
export default {
  name: "ArticleCard",
  props: {
    article: {
      type: Object,
      required: true,
    },
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

<style scoped></style>
