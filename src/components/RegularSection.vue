<style>
.regular-section {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  justify-content: start;
  gap: 16px;
  background: var(--white);
}
</style>

<template>
  <section class="regular-section">
    <slot></slot>
  </section>
</template>
