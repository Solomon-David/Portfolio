<script setup>
import { ref } from "vue";

const props = defineProps({
  src: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    required: true,
    validator: (value) => {
      return ["desktop", "mobile"].includes(value);
    },
  },
  alt: { type: String, required: true },
});

const open = ref(false);
</script>

<template>
  <div :class="props.type">
    <img :src="props.src" :alt="props.alt" @click="open = !open" />
  </div>

  <Teleport to="body">
    <Transition>
      <div class="modal" v-if="open" @click="open = !open">
        <div :class="props.type">
          <img :src="props.src" :alt="props.alt" />
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
.modal {
  position: fixed;
  z-index: 15;
  top: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 100vw;
  max-height: 100vh;
  background-color: #22222288;
}

.modal:has(.desktop) {
  padding: 75% 5%;
}

.modal:has(.mobile) {
  padding: 75% 47%;
}

.modal > div {
  position: relative;
}

.modal > .mobile {
  transform: scale(2);
}

.v-leave-to:has(.mobile),
.v-enter-from:has(.mobile) {
  transform-origin: 80% 50%;
}

.v-leave-to,
.v-enter-from {
  background-color: transparent;
  padding: 0;
  transform: scale(0.5);
}

.v-enter-active,
.v-leave-active {
  transition: all 0.5s ease;
}

.desktop {
  width: 90%;
  border: 1px solid grey;
  border-radius: 5px;
  padding: 1px;
  background-color: #222222;
}

.desktop img {
  width: 100%;
}

.mobile {
  background-color: #222222;
  padding: 2.5px;
  width: 15vw;
  aspect-ratio: 1/1;
  position: absolute;
  border: 2px solid grey;
  padding-top: 5px;
  padding-bottom: 7.5px;
  border-radius: 10px;
  right: 0;
  bottom: -3vh;
}

.mobile img {
  width: 100%;
}

@media screen and (min-width: 450px) {
  .modal:has(.desktop) {
    padding: 12% 20%;
  }

  .modal:has(.mobile) {
    padding: 14% 50%;
  }
  .mobile {
    width: 10vw;
    right: 0;
    bottom: -0.5vh;
  }
}
</style>
