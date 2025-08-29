<script setup>
const props = defineProps({
  title: String,
  description: String,
  desktopImage: String,
  mobileImage: String,
  url: String,
  urlImage: String,
});
</script>

<template>
  <article>
    <div class="images">
      <div class="desktop">
        <img :src="props.desktopImage" :alt="props.title + ' desktop image'" />
      </div>
      <div class="mobile">
        <img :src="props.mobileImage" :alt="props.title + ' mobile image'" />
      </div>
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
  width: 80vw;
  position: relative;
  display: inline;
}

.desktop img {
  width: 100%;
}

.mobile {
  height: 80%;
  position: absolute;
  border-radius: 20px;
  right: 1vw;
  bottom: 1vh;
}

.mobile img {
  width: 100%;
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
</style>
