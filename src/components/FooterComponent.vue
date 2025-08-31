<script setup>
import background from "@assets/Footerbackground.svg";
import RegularSection from "@components/RegularSection.vue";
import SectionHeading from "@components/SectionHeading.vue";
import SMIcon from "@components/SMIcon.vue";

const backgroundUrl = `url("${background}")`;
import githubImage from "@assets/GitHub.svg";
import whatsAppImage from "@assets/WhatsApp.svg";
import gmailImage from "@assets/Gmail.svg";
import linkedinImage from "@assets/LinkedIn.svg";

//socials

const socials = [
  {
    title: "WhatsApp",
    image: whatsAppImage,
    link: "https://wa.me/+2348135021023",
  },
  {
    title: "Github",
    image: githubImage,
    link: "https://github.com/Solomon-David",
  },
  {
    title: "Gmail",
    image: gmailImage,
    link: "mailto:sakesobia@gmail.com",
  },
  {
    title: "LinkedIn",
    image: linkedinImage,
    link: "https://www.linkedin.com/in/solomondavid-akesobia",
  },
];

import { useTemplateRef, inject, onMounted } from "vue";
const navobserver = inject("navobserver");
const footer = useTemplateRef("footer");
onMounted(() => {
  navobserver.observe(footer.value);
});
</script>

<template>
  <footer :style="{ backgroundImage: backgroundUrl }" id="footer" ref="footer">
    <div class="footer">
      <SectionHeading
        colorscheme="var(--white)"
        subtitle="Contact me on any of these social media platforms"
        subcolor="var(--white)"
        >Contact Me</SectionHeading
      >

      <div class="icons">
        <SMIcon
          v-for="social in socials"
          :title="social.title"
          :link="social.link"
          :image="social.image"
        />
      </div>
    </div>
  </footer>
</template>

<style>
footer {
  padding: 0;
  background-repeat: no-repeat;
  height: max-content;
}

.footer {
  width: 80%;
  height: 90%;
  padding: 15% 10% 10%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  justify-content: start;
  gap: 60px;
}

.icons {
  display: flex;
  align-items: center;
  width: 100%;
  justify-content: space-evenly;
}
</style>
