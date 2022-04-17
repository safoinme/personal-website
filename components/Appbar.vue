<template>
  <v-app-bar app elevation="0" color="black">
    <v-toolbar-title class="white--text">Hamza Mogni</v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn text dark>Test</v-btn>
    <v-btn text dark>Test</v-btn>
    <v-btn text dark>Test</v-btn>
  </v-app-bar>
</template>

<script>
export default {
  name: "Appbar",

  data() {
    return {
      buttons: [
        { text: "Home", to: "" },
        { text: "Blog", to: "" },
        { text: "Resume", to: "" },
        { text: "Projects", to: "" },
      ],
    };
  },
};
</script>

<style scoped></style>
