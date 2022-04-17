<template>
  <v-app>
    <Appbar />
    <v-main>
      <v-container fluid>
        <v-row justify="center">
          <v-col cols="2">
            <Sidebar />
          </v-col>

          <v-col cols="8">
            <Nuxt />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content("articles", params.slug).fetch();

    return { article };
  },
};
</script>
