<template>
  <v-app>
    <Appbar />
    <v-main>
      <v-container fluid>
        <v-row justify="center">
          <v-col cols="2">
            <Sidebar />
          </v-col>

          <v-col cols="6">
            <Nuxt />
          </v-col>
          <v-col cols="2">
            <p class="text-h5">Categories</p>
            <p v-for="i in 10" class="subtitle-1 font-weight-regular ma-0 pa-0">
              test
            </p>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>
