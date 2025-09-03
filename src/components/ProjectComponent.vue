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
  <article>
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
        <a :href="props.url">
          <h3>{{ props.title }}</h3>
          <img class="urlimg" :src="props.urlImage" :alt="props.urlImage" />
        </a>
      </div>

      <div class="desc">
        <p>{{ props.description }}</p>
      </div>
    </div>
  </article>
</template>

<style>
article {
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

.title a {
  width: fit-content;
  display: flex;
  gap: 2vw;
  text-decoration: none;
  border-bottom: 1px solid var(--text-grey);
  padding-bottom: 1px;
}

.text {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.urlimg {
  width: 2rem;
}

@media screen and (min-width: 450px) {
  .images {
    width: 60vw;
  }
}
</style>
