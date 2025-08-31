<script setup>
import HomePage from "./views/Home.vue";
import { ref, provide, onMounted, onUnmounted, useTemplateRef } from "vue";

//setting up skill observer
const skilloptions = {
  root: null,
  rootMargin: "-45% 0px -45% 0px",
  threshold: 0,
};

let skillobserver = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      entry.target.classList.add("bigger");
    } else {
      entry.target.classList.remove("bigger");
    }
  });
}, skilloptions);

//setting up navigation observer
const currentSection = ref("");
const navoptions = {
  root: null,
  rootMargin: "-60% 0% -30% 0%",
  threshold: 0,
};

let navobserver = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      currentSection.value = entry.target.id;
    }
  });
}, navoptions);

//provided artefacts
onMounted(() => {});
const changeSection = (value) => {
  document.querySelector(value).scrollIntoView();
  // window.location.replace("#hero", "#" + value);
};
provide("skillobserver", skillobserver);
provide("navobserver", navobserver);
provide("currentSection", currentSection);
provide("changeSection", changeSection);

onUnmounted(() => {
  navobserver.disconnect();
  skillobserver.disconnect();
});
</script>

<template>
  <HomePage />
</template>

<style href="./../style.css"></style>
