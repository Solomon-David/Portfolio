<template>
  <section class="floating-card-section">
    <slot></slot>
  </section>
</template>

<script setup></script>

<style>
.floating-card-section {
  position: relative;
  padding: 4vh 5vw;
  width: 70vw !important;
  border: 1px solid var(--grey);
  border-radius: 10px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1vh;
  box-shadow: 0 4px 4px 0 var(--grey);
}

p {
  margin-bottom: 1.5vh;
}

p::last-of-type {
  margin-bottom: 0;
}

@media (min-width: 450px) {
  .floating-card-section {
    width: 60vw !important;
    gap: 4vh;
  }
}
</style>
