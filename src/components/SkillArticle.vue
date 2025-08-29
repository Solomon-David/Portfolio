<script setup>
// import { ref, useTemplateRef, onMounted } from "vue";
const props = defineProps({
  icon: String,
  title: String,
  skills: Array,
});

// const observed = ref(null);
// const image = useTemplateRef("image");
// let observer = null;
// onMounted(() => {
//   const options = {
//     root: null,
//     rootMargin: "-40% 0px -20% 0px",
//     threshold: 0.75,
//   };
//   observer = new IntersectionObserver((entries) => {
//     entries.forEach((entry) => {
//       if (entry.isIntersecting) {

//         observed.value = entry.target;
//         observed.value.classList.add("bigger");
//         console.log(observed.value);
//         observer.unobserve(observed.value);
//       }
//     });
//   }, options);

//   if (observed.value) observer.observe(observed.value);
// });
</script>

<template>
  <article class="skill">
    <div class="skill-head">
      <div class="skill-icon" ref="image">
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
}

.skill-icon {
  width: 80px;
  height: 80px;
}

.skill-icon img {
  width: 100%;
}

.bigger {
  width: 120px;
  height: auto;
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
