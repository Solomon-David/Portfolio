<script setup>
const props = defineProps({
  role: String,
  company: String,
  start: Date,
  end: Date,
  achievements: [String],
});
</script>

<template>
  <article class="experience">
    <div class="experience-head">
      <p class="top">
        <span class="role">{{ props.role }}</span> <span class="separator"> | </span>
        <span class="company">{{ props.company }}</span>
      </p>
      <p class="bottom">{{ props.start }} - {{ props.end }}</p>
    </div>

    <ul class="experience-list">
      <li v-for="acheivement in props.achievements">{{ acheivement }}</li>
    </ul>
  </article>
</template>

<style scoped>
.experience {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 1vw;
}

.experience-head {
  display: flex;
  flex-direction: column;
  /* text-wrap: nowrap; */
  line-height: 1;
}

.top *:not(.role) {
  font-weight: var(--semibold);
  color: var(--accent);
}

.separator {
  font-weight: bold;
  font-size: var(--heading-size);
}

.top {
  text-transform: capitalize;
}

.company {
  text-align: right;
}

.bottom {
  font-weight: 400;
  font-size: var(--body-size);
  color: var(--text-grey);
}

.experience-list {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.experience-list li {
  width: 80%;
  position: relative;
}

.experience-list li::marker {
  color: var(--primary);
}
</style>
