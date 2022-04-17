<template>
  <span>
    <v-card flat :to="`/blog/` + article.slug" hover>
      <div class="font-weight-thin">{{ formatDate(article.createdAt) }}</div>

      <p class="text-h4 text--primary">
        {{ article.title }}
      </p>

      <v-img :src="article.img" max-height="200px"></v-img>

      <div class="text-primary my-5">{{ article.description }}...</div>

      <v-card-actions>
        <v-btn color="black" dark :to="`/blog/` + article.slug">
          Read More
        </v-btn>
      </v-card-actions>
    </v-card>

    <v-divider class="my-5"></v-divider>
  </span>
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
        hour: "numeric",
      };
      return new Date(date).toLocaleDateString("en", options);
    },
  },
};
</script>

<style scoped></style>
