<script setup>
import RegularSection from "@components/RegularSection.vue";
import FloatingCardSection from "@components/FloatingCardSection.vue";
import SectionHeading from "@components/SectionHeading.vue";

import ChangingText from "@components/ChangingText.vue";
import profile from "@assets/profile.png";

//skills
import SkillArticle from "@components/SkillArticle.vue";
// importing skill images
import frontendIcon from "@assets/frontend.svg";
import backendIcon from "@assets/backend.svg";
import databasesIcon from "@assets/databases.svg";
import mobileIcon from "@assets/mobile.svg";
import desktopIcon from "@assets/desktop.svg";
import othersIcon from "@assets/others.svg";

//vue components
import { ref, useTemplateRef, onMounted, inject } from "vue";

//list of sections
const sections = [
  useTemplateRef("hero"),
  useTemplateRef("about"),
  useTemplateRef("skills"),
  useTemplateRef("projects"),
  useTemplateRef("experiences"),
];

//defining skill objects and skill array
const frontend = {
  icon: frontendIcon,
  title: "frontend",
  skills: ["HTML", "CSS", "JavaScript", "VueJS"],
};
const backend = { icon: backendIcon, title: "backend", skills: ["NodeJS", "ExpressJS"] };
const mobile = {
  icon: mobileIcon,
  title: "mobile",
  skills: ["Java(Android)", "Kotlin(Android)", "Flutter"],
};
const databases = {
  icon: databasesIcon,
  title: "databases",
  skills: ["MongoDB", "MySQL"],
};
const desktop = {
  icon: desktopIcon,
  title: "desktop",
  skills: ["ElectronJS", "Flutter"],
};
const others = {
  icon: othersIcon,
  title: "others",
  skills: ["TypeScript", "Quasar", "Git", "Figma"],
};
const skills = [frontend, backend, databases, mobile, desktop, others];

//Projects
import ProjectComponent from "@components/ProjectComponent.vue";
import arrow from "@assets/arrow.svg";
//importing project images
import SRASPC from "@assets/SRASPC.png";
import SRASMobile from "@assets/SRASMobile.png";
import WeTechPC from "@assets/WeTechPC.png";
import WeTechMobile from "@assets/WeTechMobile.png";
import ExperienceComponent from "./ExperienceComponent.vue";

const projects = [
  {
    desktopImage: SRASPC,
    mobileImage: SRASMobile,
    title: "SRAS",
    description:
      "A course reporting and result assessing system for students and lecturers",
    url: "https://frank-ezeilo-s-project.onrender.com",
  },
  {
    desktopImage: WeTechPC,
    mobileImage: WeTechMobile,
    title: "WeTech",
    description:
      "A micro-blogging platform for techies. Co-created by I and my colleagues during my Industrial Training at Harvoxx Tech Hub.",
    url: "wetech-p7y7.onrender.com/home",
  },
];

// Experiences
const experiences = [
  {
    role: "coding instructor",
    company: "Dreckline Technologies",
    start: "February 2025",
    end: "May 2025",
    achievements: [
      "Instructed children on desktop, web, and native Android development",
      "Assisted and supervised trainees and staff on installation of software packages",
    ],
  },
  {
    role: "frontend intern",
    company: "harvoxx tech hub",
    start: "May 2023",
    end: "December 2023",
    achievements: [
      "Learned and taught frontend technologies including CSS and JavaScript",
      "Collaborated in group projects",
    ],
  },
];

// for mounted codes
let navobserver = inject("navobserver");
const changeSection = inject("changeSection");

onMounted(() => {
  sections.forEach((section) => {
    navobserver.observe(section.value.$el);
  });
});
</script>

<template [style]="./../style.css">
  <main>
    <!-- Hero section -->
    <regular-section id="hero" ref="hero" class="hero">
      <div class="intros">
        <p class="intro">Hello, I'm <span>Solomon</span>David</p>
        <ChangingText fixed="Developer" :options="['web', 'mobile', 'desktop']" />
        <p class="end">
          A developer and instructor here to help you reach your every goal.
        </p>
      </div>

      <div class="myimage">
        <img :src="profile" alt="myimage" />
      </div>

      <div class="contactme">
        <button @click="changeSection('footer')">contact me</button>
      </div>
    </regular-section>

    <!-- About section -->
    <floating-card-section id="about" ref="about">
      <section-heading>about me</section-heading>
      <article>
        <p>I am <b>SolomonDavid Akesobia</b> by name.</p>
        <p>
          I am based in the city of Port Harcourt, <b>Nigeria</b>, but open to remote
          projects.
        </p>
        <p>
          I began my development journey in <b>2018</b> when I started learning C++ in a
          bid to understand the science behind how applications were built. Being mostly
          interested in applications, I learned Java and later ventured into native
          <b>Android</b> application development for a while before having to switch to
          web development due to technological constraints.
        </p>
        <p>
          As a web developer, I was always drawn more to logic than asthetics and soon
          began learning backend development with NodeJS and Express. I ventured into full
          stack development and dabbled in the MEAN stack until a project necessitated me
          learning Vue, after which I fell in love with Vue's power and simplicity. Ever
          since, I had stuck to the MEVN tech stack.
        </p>
        <p>
          In a bid to expand my horizons, I tried my hand with ElectronJS for desktop
          applications and NativeScript for mobile development. Dissatisfied with
          Electron's performance tradeoffs and NativeScript's lack of maturity, I replaced
          them with JavaFX and Kotlin respectively for a while, returning back to my JVM
          roots. However, simultaneously learning multiple frameworks for different
          platforms was tedious and so I needed to change my tech stack yet again. That's
          when I discovered Flutter and stuck to it: a decision I am yet to regret!
        </p>
        <p>
          Aside from being a developer, I have a B.Sc in <b>Computer Science</b> from the
          Rivers State University.
        </p>
        <p>My hobbies include gaming, gymnastics, swimming, and reading.</p>
      </article>
    </floating-card-section>

    <!-- Skills -->
    <regular-section id="skills" ref="skills">
      <section-heading subtitle="Here are some of my most prominent skills."
        >skills</section-heading
      >
      <div class="skills">
        <SkillArticle
          v-for="skill in skills"
          :key="skill.title"
          :icon="skill.icon"
          :title="skill.title"
          :skills="skill.skills"
        />
      </div>
    </regular-section>

    <!-- Projects -->
    <floating-card-section id="projects" ref="projects">
      <section-heading subtitle="Here are some projects I have worked on over the years."
        >projects</section-heading
      >
      <div class="projects scrollable">
        <ProjectComponent
          v-for="project in projects"
          :title="project.title"
          :url="project.url"
          :description="project.description"
          :desktopImage="project.desktopImage"
          :mobileImage="project.mobileImage"
          :urlImage="arrow"
        />
      </div>
    </floating-card-section>

    <regular-section id="experiences" ref="experiences">
      <section-heading subtitle="A few organizations I have worked with over the years">
        Experiences
      </section-heading>
      <div class="experiences">
        <ExperienceComponent
          v-for="exp in experiences"
          :role="exp.role"
          :company="exp.company"
          :start="exp.start"
          :end="exp.end"
          :achievements="exp.achievements"
        />
      </div>
    </regular-section>
  </main>
</template>

<style scoped>
main {
  padding: 15vh 1rem 10vh;
  height: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0;
  gap: 12vh;
}

section {
  width: 80vw;
}

/* hero section*/

.hero {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  gap: 100px;
  background: var(--white);
}
/* intro*/

.intro {
  font-size: calc(var(--body-size) * 1.2);
}

.intro span {
  color: var(--accent);
  font-weight: var(--medium);
}

.intros {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 8px;
}

.end {
  width: 55vw;
}

.myimage {
  width: 50vw;
  transform: scale(1.25);
  aspect-ratio: 1/1;
  border-radius: 200px;
  outline: 1px solid var(--grey);
  background: var(--grey);
  outline-offset: 20px;

  overflow: hidden;
}

.myimage img {
  width: 100%;
  max-height: inherit;
  object-fit: cover;
  object-position: 0px -5vw;
  filter: saturate(0);
}

/* Contact me button*/
.contactme button {
  background-color: var(--primary);
  color: var(--white);
  font-size: var(--heading-size);
  border: none;
  border-radius: 10px;
  padding: 1rem;
  font-weight: var(--medium);
  text-transform: capitalize;
  cursor: pointer;
}

.contactme button:hover {
  background-color: var(--accent);
  background-color: var(--white);
  color: var(--accent);
  border: 1px solid var(--accent);
  transition: background-color 0.3s ease;
}

/* About */
#about article {
  display: flex;
  flex-direction: column;
  gap: 1.5vh;
  font-size: var(--body-size);
  line-height: 1.6;
}

/*Skills*/
.skills {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 5vh;
}
/* Projects */
.projects {
  width: 100%;
  display: flex;
  justify-content: start;
  gap: 5vw;
  overflow-x: scroll;
}

/* Experiences */
.experiences {
  display: flex;
  flex-direction: column;
  gap: 3vh;
}
</style>
