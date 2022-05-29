<template>
  <v-app-bar app elevation="0" color="transparent" class="mx-16 px-16" absolute>
    <v-toolbar-title>
      <v-btn href="/" text class="text-h6 font-weight-black">
        Safoine El Khabich
      </v-btn>
    </v-toolbar-title>
    <!-- <v-spacer></v-spacer>
    <v-btn text>Test</v-btn>
    <v-btn text>Test</v-btn>
    <v-btn text>Test</v-btn> -->
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
