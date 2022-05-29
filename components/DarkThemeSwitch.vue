<template>
  <v-btn icon x-large @click.prevent="switchTheme">
    <v-icon>{{ icon }}</v-icon>
  </v-btn>
</template>

<script>
import { mdiWeatherNight, mdiWhiteBalanceSunny } from "@mdi/js";
export default {
  computed: {
    icon: function () {
      return this.$vuetify.theme.dark ? mdiWhiteBalanceSunny : mdiWeatherNight;
    },
  },

  methods: {
    switchTheme() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
  },
};
</script>

<style></style>
