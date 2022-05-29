<template>
  <v-row justify="center">
    <v-col v-for="(social, idx) in social_media" :key="idx" class="flex-grow-0">
      <v-btn icon :href="social.href" target="_blank">
        <v-icon>{{ social.icon }}</v-icon>
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      social_media: [
        { icon: "mdi-github", href: "https://github.com/safoinme" },
        { icon: "mdi-linkedin", href: "https://www.linkedin.com/in/safoinme" },
        { icon: "mdi-twitter", href: "https://twitter.com/safoinme" },
      ],
    };
  },
};
</script>

<style></style>
