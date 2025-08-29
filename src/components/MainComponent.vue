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
</script>

<template [style]="./../style.css">
  <main>
    <!-- Hero section -->
    <section id="hero" class="hero">
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
        <button>contact me</button>
      </div>
    </section>

    <!-- About section -->
    <floating-card-section id="about">
      <section-heading>about me</section-heading>
      <article>
        <p>I am <b>SolomonDavid Akesobia</b> by name.</p>
        <p>
          I am based in the city of Port Harcourt, <b>Nigeria</b>, but open to remote
          projects.
        </p>
        <p>I have a B.Sc in <b>Computer Science</b> from the Rivers State University.</p>
        <p>I am both a team player and a lone wolf when it comes to solving problems.</p>
      </article>
    </floating-card-section>

    <!-- Skills -->
    <regular-section id="skills">
      <section-heading subtitle="Here are some of my most prominent skills."
        >skills</section-heading
      >
      <div class="skills">
        <SkillArticle
          v-for="skill in skills"
          :icon="skill.icon"
          :title="skill.title"
          :skills="skill.skills"
        />
      </div>
    </regular-section>

    <!-- Projects -->
    <floating-card-section id="projects">
      <section-heading subtitle="Here are some projects I have worked on over the years."
        >projects</section-heading
      >
      <div class="projects">
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

    <regular-section id="experiences">
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
  padding: 1vh 1rem 10vh;
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
  overflow: scroll;
}

/* Experiences */
.experiences {
  display: flex;
  flex-direction: column;
  gap: 3vh;
}
</style>
