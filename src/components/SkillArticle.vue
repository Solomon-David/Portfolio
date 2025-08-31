<script setup>
import { useTemplateRef, onMounted, onUnmounted, inject } from "vue";
const props = defineProps({
  icon: String,
  title: String,
  skills: Array,
});

const article = useTemplateRef("article");
const observer = inject("skillobserver");
onMounted(() => {
  observer.observe(article.value);
});

defineExpose({
  title: props.title,
});
</script>

<template>
  <article class="skill" ref="article">
    <div class="skill-head">
      <div class="skill-icon">
        <img :src="props.icon" :alt="props.icon" />
      </div>

      <div class="skill-title">
        <h3>{{ props.title }}</h3>
      </div>
    </div>

    <ul class="skill-body">
      <li v-for="skill in props.skills">{{ skill }}</li>
    </ul>
  </article>
</template>

<style scoped>
.skill {
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
  gap: 4px;
  transition: transform 0.3s ease;
}

.skill-icon {
  width: 80px;
  height: 80px;
}

.skill-icon img {
  width: 100%;
}

.bigger {
  transform: scale(1.2);
}

.skill-head {
  display: flex;
  flex-direction: column;
  justify-content: end;
  align-items: center;
  gap: 1vh;
  text-transform: capitalize;
}

.skill li {
  list-style: none;
  line-height: 1.5;
  text-align: center;
}
</style>
