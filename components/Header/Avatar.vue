<template>
  <v-avatar size="150px" class="mb-4">
    <v-img :src="src"></v-img>
  </v-avatar>
</template>
<script>
export default {
  props: {
    src: {
      type: String,
      required: true,
    },
  },
};
</script>
