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
      "A course reporting and result assessing system for students and lecturers. Developed using Vue, ExpressJS, and MySQL.",
    url: "https://frank-ezeilo-s-project.onrender.com",
  },
  {
    desktopImage: WeTechPC,
    mobileImage: WeTechMobile,
    title: "WeTech",
    description:
      "A micro-blogging platform for techies. Co-created by I and my colleagues during my Industrial Training at Harvoxx Tech Hub. The backend was co-developed by me using Express, Mongoose, and EJS.",
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
          <ChangingText fixed="Developer" :options="['web', 'mobile', 'desktop']" />
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
            I am <b>SolomonDavid Akesobia-Nkom</b>, a developer based in Port Harcourt,
            <b>Nigeria</b>, with a B.Sc. in Computer Science from Rivers State University.
          </p>

          <p>
            I have been a programming since <b>2018</b>, when I started learning C++ and
            Java before moving into <b>Web Development</b>. Drawn to backend logic, I
            learned <b>NodeJS</b> and <b>Express</b>. Over time, I explored several
            frontend technologies and eventually settled on Vue due to its ease of use and
            seamless integration.
          </p>

          <p>
            Web development aside, I also played around with <b>ElectronJS</b> and Java
            for desktop application and native Android development respectively. In order
            to use a single technology for both platforms, I adopted <b>Flutter</b> as my
            cross-platform solution, and it has been my choice ever since.
          </p>

          <p>
            Aside from coding, I am also an <b>Instructor</b> capable of handling
            one-on-one and group tutorials. I specialize in coding and mathematics and can
            tutor both children and adults.
          </p>

          <p>
            When I am not coding, I enjoy gaming, gymnastics, martial arts tricking,
            swimming, and reading.
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
  display: flex;
  justify-content: start;
  gap: 5vw;
  overflow-x: scroll;
}

/* Experiences */
.experiences {
  display: grid;
  grid-template-columns: 1fr;
  gap: 5vh;
}

@media screen and (max-width: 374px) {
  .myimage {
    width: 150px;
  }

  .imgwrp {
    padding: 20px;
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
