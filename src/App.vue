<script setup>
import HomePage from "./views/Home.vue";
import { ref, provide, onMounted, onUnmounted, computed } from "vue";

//checking screen size
const width = ref(visualViewport ? visualViewport.width : innerWidth);
const isMobile = computed(() => width.value < 450);
const resized = () => {
  width.value = visualViewport ? visualViewport.width : innerWidth;
};

//setting up skill observer
const skilloptions = {
  root: null,
  rootMargin: "-55% 0px -45% 0px",
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

onMounted(() => {
  window.addEventListener("resize", resized);
});

//provided artefacts
const changeSection = (value) => {
  document.querySelector(value).scrollIntoView();
  // window.location.replace("#hero", "#" + value);
};
provide("skillobserver", skillobserver);
provide("navobserver", navobserver);
provide("currentSection", currentSection);
provide("changeSection", changeSection);
provide("isMobile", isMobile);

onUnmounted(() => {
  navobserver.disconnect();
  skillobserver.disconnect();
  window.RemoveEventListener("resize", resized);
});
</script>

<template>
  <HomePage />
</template>

<style href="./../style.css"></style>
