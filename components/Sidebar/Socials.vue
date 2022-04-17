<template>
  <v-row>
    <v-btn icon v-for="icon in icons" :key="icon.name">
      <v-icon class="mx-1" color="grey">{{ icon.name }}</v-icon>
    </v-btn>
  </v-row>
</template>

<script>
export default {
  name: "Socials",

  data() {
    return {
      icons: [
        { name: "mdi-twitter", link: "" },
        { name: "mdi-linkedin", link: "" },
        { name: "mdi-github", link: "" },
      ],
    };
  },
};
</script>

<style scoped></style>
