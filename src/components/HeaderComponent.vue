<script setup>
import logo from "@assets/logo.png";
import NavComponent from "@components/NavComponent.vue";
import { ref, inject } from "vue";

const currentSection = inject("currentSection");

const height = ref("2vh");
</script>

<template>
  <Transition name="grow">
    <header
      :style="{
        borderBottom: currentSection === 'hero' ? 'none' : '1px solid var(--grey)',
        height,
      }"
    >
      <div id="logo">
        <img :src="logo" alt="no" />
      </div>

      <NavComponent @open="(open) => (height = open ? '45vh' : '8vh')" />
    </header>
  </Transition>
</template>

<style scoped>
header {
  padding: 1vh 5vw 2vh;
  display: grid;
  grid-template-columns: 1fr 1fr;
  width: 90vw;
  justify-content: space-between;
  align-items: start;
  background-color: var(--background);
  position: fixed;
  top: 0;
  z-index: 2;
  transition: height 0.3s ease-in-out;
}

#logo img {
  height: 32px;
  width: auto;
  margin: 10px;
}

.grow-enter-from,
.grow-leave-to {
  transform-origin: top;
  height: 2vh;
  opacity: 0;
}

.grow-leave-from,
.grow-enter-to {
  transform-origin: top;
  opacity: 1;
  height: 5vh;
}

.grow-enter-active,
.grow-leave-active {
  transition: all 0.3s ease;
}

@media screen and (min-width: 450px) {
  header {
    grid-template-columns: 1fr 1fr 1fr;
    padding: 2vh 3vw;
    justify-content: center;
  }
}
</style>
