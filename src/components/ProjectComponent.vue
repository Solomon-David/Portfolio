<script setup>
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
  width: 70vw;
  height: 100%;
  position: relative;
  display: inline;
  margin: 0;
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

  .mobile {
    width: 10vw;
    right: 0;
    bottom: -0.5vh;
  }
}
</style>
