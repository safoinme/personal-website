<template>
  <nav>
    <ul>
      <li v-for="link of toc" :key="link.id">
        <NuxtLink :to="`#${link.id}`">{{ link.text }}</NuxtLink>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "TableOfContents",

  props: {
    "toc": {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>

</style>
