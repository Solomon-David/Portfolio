<template>
  <a target="_blank" :href="link">
    <img :src="image" :alt="title" />
  </a>
</template>

<style>
a {
  width: fit-content;
}
img {
  width: 40px;
}
</style>

<script setup>
const props = defineProps({
  link: String,
  image: String,
  title: String,
});
</script>
