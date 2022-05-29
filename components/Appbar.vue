<template>
  <v-app-bar app elevation="0" color="transparent" class="mx-16 px-16" absolute>
    <v-toolbar-title>
      <v-btn href="/" text class="text-h6 font-weight-black text-capitalize">
        Safoine El Khabich
      </v-btn>
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <v-btn v-for="(btn, idx) in buttons" :key="idx" text>
      {{ btn.text }}
    </v-btn>
    <DarkThemeSwitch/>
  </v-app-bar>
</template>

<script>
import DarkThemeSwitch from './DarkThemeSwitch.vue';
export default {
    name: "Appbar",
    data() {
        return {
            buttons: [
                { text: "Home", to: "/" },
                { text: "Resume", to: "" },
                { text: "Projects", to: "" },
            ],
        };
    },
    components: { DarkThemeSwitch }
};
</script>

<style scoped></style>
