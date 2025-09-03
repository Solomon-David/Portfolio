<script setup>
import { ref, onMounted } from "vue";
const props = defineProps({
  options: {
    type: Array,
    required: true,
  },
  fixed: {
    type: String,
  },
});

const option = ref(props.options[0]);
const index = ref(0);
setInterval(() => {
  index.value = (index.value + 1) % props.options.length;
  option.value = props.options[index.value];
}, 2500);
</script>

<template>
  <div class="changing-text">
    <h1>
      <Transition name="change">
        <span :key="option">{{ option }}</span>
      </Transition>
      <br />
      {{ fixed }}
    </h1>
  </div>
</template>

<style>
.change-enter-from,
.change-leave-to {
  opacity: 0;
}

.change-enter-to,
.change-leave-from {
  opacity: 1;
}

.change-enter-active,
.change-leave-active {
  transition: opacity 1s ease;
  position: absolute;
}

h1 {
  font-size: calc(var(--heading-size) * 1.5);
  font-weight: 900;
  line-height: 1;
}

h1 span {
  text-transform: capitalize;
  color: var(--accent);
}

@media (min-width: 450px) {
  h1 {
    font-size: calc(var(--heading-size) * 2.5);
  }
}
</style>
