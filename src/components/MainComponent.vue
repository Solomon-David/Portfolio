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
import { ref, useTemplateRef, onMounted, inject, nextTick } from "vue";

//list of sections
const sections = [
  useTemplateRef("heroRef"),
  useTemplateRef("aboutRef"),
  useTemplateRef("skillsRef"),
  useTemplateRef("projectsRef"),
  useTemplateRef("experiencesRef"),
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
  skills: ["ElectronJS", "Flutter", "JavaFX"],
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
import TrackFastMobile from "@assets/TrackfastMobile.png";
import TrackFastPC from "@assets/TrackfastPC.png";
import FintrackMobile from "@assets/Fintrack-mobile.jpeg";
import FintrackDesktop from "@assets/Fintrack-desktop.jpeg";

const projects = [
  {
    desktopImage: SRASPC,
    mobileImage: SRASMobile,
    title: "SRAS",
    description:
      "A course reporting and result assessing system for students and lecturers. Developed using Vue, ExpressJS, and MySQL.",
    url: "https://frank-ezeilo-s-project.onrender.com",
  },
  {
    desktopImage: WeTechPC,
    mobileImage: WeTechMobile,
    title: "WeTech",
    description:
      "A micro-blogging platform for techies. Co-created by I and my colleagues during my Industrial Training at Harvoxx Tech Hub. The backend was co-developed by me using Express, Mongoose, and EJS.",
    url: "https://wetech-p7y7.onrender.com/home",
  },
  {
    desktopImage: TrackFastPC,
    mobileImage: TrackFastMobile,
    title: "TrackFast",
    description:
      "A delivery tracking system for customers and delivery agents. It calculates costs using the actual distance between the locations and provides a 3-layer RBAC. \n Developed using Vuetify, Express, and MongoDB.",
    url: "https://trackfast-frontend.onrender.com",
  },
  {
    desktopImage: FintrackDesktop,
    mobileImage: FintrackMobile,
    title: "Fintrack",
    description:
      "FinTrack is a personal finance management application for tracking income, expenses, recurring bills, savings plans, and periodic financial summaries. \n It is built as an installable Progressive Web App (PWA) with a Vue, Express, and MongoDB.",
    url: "https://fin-track-three-coral.vercel.app/",
  },
];

const projectsContainer = ref(null);

const showLeft = ref(false);
const showRight = ref(true);

function handleProjectScroll() {
  const container = projectsContainer.value;

  if (!container) return;

  const scrollLeft = container.scrollLeft;
  const maxScrollLeft = container.scrollWidth - container.clientWidth;
  const firstCard = container.querySelector(".project-card");
  const lastCard = container.querySelector(".project-card:last-of-type");

  showLeft.value = scrollLeft > 10;

  if (lastCard) {
    const containerRect = container.getBoundingClientRect();
    const lastCardRect = lastCard.getBoundingClientRect();
    const isLastCardVisible =
      lastCardRect.right > containerRect.left + 10 &&
      lastCardRect.left < containerRect.right - 10;

    showRight.value = !isLastCardVisible && scrollLeft < maxScrollLeft - 10;
    return;
  }

  showRight.value = scrollLeft < maxScrollLeft - 10;
}

function scrollProjects(direction) {
  const container = projectsContainer.value;

  if (!container) return;

  const firstCard = container.querySelector(".project-card");
  const lastCard = container.querySelector(".project-card:last-of-type");

  const scrollAmount = firstCard?.offsetWidth || container.clientWidth * 0.8;

  container.scrollBy({
    left: direction === "right" ? scrollAmount : -scrollAmount,
    behavior: "smooth",
  });
}

onMounted(async () => {
  await nextTick();
  handleProjectScroll();
});

//Experience
import ExperienceComponent from "./ExperienceComponent.vue";
const experiences = [
  {
    role: "coding instructor",
    company: "Dreckline Technologies",
    start: "February 2025",
    end: "May 2025",
    achievements: [
      "Instructed students aged 8–15 in desktop, web, and native Android application development.",
      "Guided and supported trainees and staff in the installation and configuration of software packages.",
    ],
  },
  {
    role: "frontend intern",
    company: "harvoxx tech hub",
    start: "May 2023",
    end: "December 2023",
    achievements: [
      "Studied and delivered instruction on front-end technologies including CSS and JavaScript.",
      "Contributed to team-based projects through active collaboration.",
      "Provided peer tutoring to address knowledge gaps and reinforce learning.",
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
    <regular-section id="hero" ref="heroRef" class="hero">
      <div class="hero-top">
        <div class="intros">
          <p class="intro">Hello, I'm <span>Solomon</span>David</p>
          <ChangingText fixed="Developer" :options="['Web', 'Mobile', 'Desktop']" />
          <p class="end">
            A developer and instructor here to help you reach your every goal.
          </p>
        </div>

        <div class="imgwrp">
          <div class="myimage">
            <img :src="profile" alt="myimage" />
          </div>
        </div>
      </div>

      <div class="contactme">
        <button @click="changeSection('footer')">contact me</button>
      </div>
    </regular-section>

    <!-- About section -->
    <floating-card-section id="about" ref="aboutRef">
      <section-heading>about me</section-heading>
      <div>
        <article>
          <p>
            I am <b>SolomonDavid Akesobia-Nkom</b>, a software developer based in Port
            Harcourt, <b>Nigeria</b>, with a Bachelor's degree in Computer Science from
            Rivers State University. I am passionate about building efficient, scalable,
            and user-focused digital solutions that solve real-world problems.
          </p>

          <p>
            My programming journey began in 2018 with <b>C++</b> and <b>Java</b>, laying a
            strong foundation in software engineering principles before transitioning into
            <b>web development</b>. Fascinated by application architecture and backend
            systems, I expanded my expertise with <b>Node.js</b> and <b>Express</b>. Along
            the way, I explored a variety of frontend technologies and ultimately chose
            <b>Vue.js</b> for its simplicity, flexibility, and seamless developer
            experience.
          </p>

          <p>
            Beyond web technologies, I have developed desktop and mobile applications
            using <b>Electron.js</b> and native Android development with <b>Java</b>.
            Seeking a unified approach to cross-platform development, I adopted
            <b>Flutter</b>, which has since become my preferred framework for building
            high-performance applications across multiple platforms.
          </p>

          <p>
            In addition to software development, I am an experienced
            <b>programming</b> and <b>mathematics</b> instructor. I have successfully
            delivered both one-on-one and group training sessions for learners of varying
            ages and skill levels, helping them build confidence and competence in their
            chosen fields.
          </p>

          <p>
            Outside of technology, I enjoy gaming, gymnastics, martial arts tricking,
            swimming, and reading. These interests help me maintain a balanced lifestyle
            while fostering the discipline, creativity, and problem-solving mindset that I
            bring to every project.
          </p>
        </article>
      </div>
    </floating-card-section>

    <!-- Skills -->
    <regular-section id="skills" ref="skillsRef">
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
    <floating-card-section id="projects" ref="projectsRef">
      <section-heading subtitle="Here are some projects I have worked on over the years.">
        projects
      </section-heading>

      <div
        class="projects scrollable"
        ref="projectsContainer"
        @scroll="handleProjectScroll"
      >
        <ProjectComponent
          v-for="project in projects.slice().reverse()"
          :key="project.title"
          :title="project.title"
          :url="project.url"
          :description="project.description"
          :desktopImage="project.desktopImage"
          :mobileImage="project.mobileImage"
          :urlImage="arrow"
        />
      </div>

      <div class="project-nav">
        <button
          :class="{ visible: !showLeft }"
          class="nav-btn"
          @click="scrollProjects('left')"
          aria-label="Previous project"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            width="24"
            height="24"
            fill="none"
            stroke="currentColor"
            stroke-width="3"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <polyline points="15 18 9 12 15 6" />
          </svg>
        </button>

        <button
          :class="{ visible: !showRight }"
          class="nav-btn"
          @click="scrollProjects('right')"
          aria-label="Next project"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            width="24"
            height="24"
            fill="none"
            stroke="currentColor"
            stroke-width="3"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <polyline points="9 18 15 12 9 6" />
          </svg>
        </button>
      </div>
    </floating-card-section>

    <regular-section id="experiences" ref="experiencesRef">
      <section-heading subtitle="A few organizations I have worked with over the years">
        Experience
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
  padding: 12vh 5vw;
  height: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: stretch;
  margin: 0;
  gap: 12vh;
  overflow-x: hidden;
}

section {
  width: 80vw;
  margin: 0 auto;
  justify-items: start;
  row-gap: 2.5vh;
}

/* hero section*/

.hero {
  display: flex;
  flex-direction: column;
  justify-content: end;
  align-items: center;
  margin: 0 auto;
  gap: 32px;
  background: var(--white);
}

.hero-top {
  display: inherit;
  flex-direction: inherit;
  gap: inherit;
  justify-content: inherit;
  align-items: inherit;
  background: inherit;
  padding: 0;
  padding-left: 0;
  width: 80%;
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

.myimage {
  width: 250px;
  aspect-ratio: 1/1;
  border-radius: 200px;
  background: var(--grey);
  overflow: hidden;
}

.imgwrp {
  margin: 0;
  border-radius: 200px;
  border: 1px solid #4338ca44;
  padding: 40px;
}

.myimage img {
  width: 100%;
  max-height: inherit;
  object-fit: cover;
  object-position: 0px -20px;
  filter: saturate(0);
}

/* Contact me button*/
.contactme {
  margin-right: 0;
}
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
  display: grid;
  grid-template-columns: 1fr;
  justify-content: space-between;
  gap: 10vh;
}
/* Projects */
.projects {
  width: 100%;
  height: max-content;
  display: flex;
  justify-content: space-evenly;
  overflow-x: scroll;
  scroll-behavior: smooth;

  scroll-snap-type: x mandatory;
}

.projects::-webkit-scrollbar {
  display: none;
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.project-nav {
  display: flex;
  justify-content: center;
  gap: 10vw;
  margin-top: 1.5rem;
}

.nav-btn {
  width: 48px;
  height: 48px;
  border: none;
  border-radius: 50%;
  cursor: pointer;

  display: flex;
  align-items: center;
  justify-content: center;

  transition: all 0.2s ease;
  background: var(--primary);
}

.nav-btn svg {
  width: 24px;
  height: 24px;
  stroke: white;
}

.nav-btn:hover {
  transform: translateY(-2px);
}

.visible {
  visibility: hidden;
}

/* Experiences */
.experiences {
  display: grid;
  grid-template-columns: 1fr;
}

.experiences article {
  max-width: fit-content;
}

@media screen and (max-width: 374px) {
  .myimage {
    width: 75vw;
  }

  .imgwrp {
    padding: 20px;
    margin-bottom: 5vh;
  }
}

@media (min-width: 450px) {
  main {
    padding: 20vh 2vw;
    gap: 24vh;
  }

  section {
    width: 90vw;
  }

  .hero {
    padding: 5vh 0vw;
    justify-content: end;
    gap: 25px;
    align-items: start;
  }

  .hero-top {
    flex-direction: row;
    width: max-content;
    height: 290px;
    gap: 24vw;
  }

  .intros {
    gap: 8px;
  }

  .myimage {
    width: 325px;
  }

  .imgwrp {
    margin: 0;
  }

  .contactme button {
    padding: 2.5vh 2vw;
    font-size: var(--body-size);
  }

  /* skills */
  .skills {
    grid-template-columns: repeat(3, 1fr);
    column-gap: 15vw;
  }

  .experiences {
    grid-template-columns: 1fr 1fr;
  }
}
</style>
