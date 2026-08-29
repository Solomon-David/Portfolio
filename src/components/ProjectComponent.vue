<script setup>
import ExpandableImage from "./ExpandableImage.vue";

const props = defineProps({
  title: String,
  description: String,
  desktopImage: String,
  mobileImage: String,
  url: String,
  urlImage: String,
});

// create modal for project images when clicked
</script>

<template>
  <article class="project-card">
    <div class="images">
      <ExpandableImage
        type="desktop"
        :src="props.desktopImage"
        :alt="props.title + ' desktop image'"
      />
      <ExpandableImage
        type="mobile"
        :src="props.mobileImage"
        :alt="props.title + ' mobile image'"
      />
    </div>

    <div class="text">
      <div class="title">
        <a
          class="title-link"
          :href="props.url.startsWith('http') ? props.url : `https://${props.url}`"
          target="_blank"
          rel="noopener noreferrer"
        >
          <h3>{{ props.title }}</h3>
          <img class="urlimg" :src="props.urlImage" alt="" />
        </a>
      </div>

      <div class="desc">
        <p>{{ props.description }}</p>
      </div>
    </div>
  </article>
</template>

<style scoped>
.project-card {
  scroll-snap-align: start;

  flex: 0 0 80vw;
}

article {
  width: 80vw;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  gap: 5vh;
}
.images {
  width: 70vw;
  height: 100%;
  position: relative;
  display: inline;
  margin: 0;
}

.title {
  justify-self: end;
}

.title-link {
  width: fit-content;
  display: flex;
  align-items: center;
  gap: 0.5rem;

  color: inherit;
  text-decoration: none;
}

.title-link h3 {
  text-decoration: underline;
  text-underline-offset: 3px;
}

.title a {
  width: fit-content;
  display: flex;
  align-items: center;
  gap: 0.5rem;

  color: var(--accent);
  text-decoration: underline;
  text-underline-offset: 3px;

  transition: opacity 0.2s ease;
}

.title a:hover {
  opacity: 0.8;
}

.text {
  display: flex;
  flex-direction: column;
  gap: 8px;
  max-width: 100%;
}

.project-link {
  color: var(--accent);
  text-decoration: underline;
  text-underline-offset: 3px;
  word-break: break-word;
}

.project-link:hover {
  opacity: 0.8;
}

.urlimg {
  width: 1rem;
  height: 1rem;
  object-fit: contain;
}

.desc p {
  max-width: 85%;
}

@media screen and (min-width: 450px) {
  .images {
    width: 60vw;
  }

  .project-card {
    flex: 0 0 60vw;
    width: 60vw;
  }
}
</style>
