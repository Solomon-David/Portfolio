<script setup>
import { inject, ref, onMounted, watchEffect, useTemplateRef } from "vue";

import menu from "@assets/Menu.svg";
import close from "@assets/Close.svg";
//checking screensize
const isMobile = inject("isMobile");
// toggling the menu
let open = ref(false);
const toggleMenu = () => {
  open.value = !open.value;
};

//using current section
const nav = useTemplateRef("nav");
const currentSection = inject("currentSection");

const emit = defineEmits(["open"]);

watchEffect(() => {
  emit("open", open.value);
});

onMounted(async () => {
  watchEffect(() => {
    nav.value.childNodes.forEach((el) => {
      if (el.href.split("#")[1] == currentSection.value) {
        el.classList.add("current");
      } else {
        el.classList.remove("current");
      }
    });
  });
});
</script>

<template>
  <div id="navcomponent">
    <div id="menu" v-if="isMobile">
      <button @click="toggleMenu">
        <span v-if="!open"
          ><img :src="menu" alt="hamburger menu to open navigation bar" />
        </span>
        <span v-if="open"
          ><img :src="close" alt="X shaped button to close navigation bar"
        /></span>
      </button>
    </div>

    <Transition name="slide">
      <nav v-show="open || !isMobile" ref="nav">
        <a @click="open = false" href="#hero">Home</a>
        <a @click="open = false" href="#about">About</a>
        <a @click="open = false" href="#skills">Skills</a>
        <a @click="open = false" href="#projects">Projects</a>
        <a @click="open = false" href="#experiences">Experience</a>
        <a @click="open = false" href="#footer">Contact</a>
      </nav>
    </Transition>
  </div>
</template>

<style scoped>
#navcomponent {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100%;
  align-items: end;
  gap: 3vh;
}

#menu button {
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.1rem;
}

#menu button img {
  width: 2rem;
  aspect-ratio: 1/1;
}

nav {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  background-color: var(--background);
  padding-left: 5vw;
  padding-bottom: 2vh;
  border-radius: 16px;
  align-items: end;
}

nav a {
  text-align: left;
  text-decoration: none;
  line-height: 1rem;
  font-weight: var(--semibold);
}

.current {
  color: var(--primary);
  font-weight: bold;
}

nav a:hover,
.current:hover {
  text-decoration: underline;
  text-decoration-thickness: 3px;
  text-underline-offset: 10px;
  text-decoration-color: var(--color);
}

.current:hover {
  text-decoration-color: var(--primary);
}
.slide-enter-from,
.slide-leave-to {
  transform-origin: top;
  transform: scaleY(0%);
  opacity: 0;
}

.slide-leave-from,
.slide-enter-to {
  transform-origin: top;
  opacity: 1;
  transform: scaleY(100%);
}

.slide-enter-active,
.slide-leave-active {
  transition: all 0.3s ease;
}

@media (min-width: 450px) {
  #navcomponent {
  }

  nav {
    flex-direction: row;
    gap: 1rem;
    align-items: center;
  }
}
</style>
