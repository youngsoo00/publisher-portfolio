<script setup>
import { computed, ref } from 'vue'
import { coreSkills, projects } from './data/projects'

const selectedYear = ref('All')
const years = ['All', ...new Set(projects.map((project) => project.year))]
const loopSkills = [...coreSkills, ...coreSkills]
const filteredProjects = computed(() => selectedYear.value === 'All'
  ? projects
  : projects.filter((project) => project.year === selectedYear.value))
</script>

<template>
  <main>
    <header class="hero" id="top">
      <nav class="hero__nav" aria-label="주요 메뉴">
        <a class="brand" href="#top"></a>
        <div>
          <a href="#skills">About</a>
          <a href="#projects">Project</a>
          <a href="mailto:imaboutthat87@gmail.com">Contact</a>
        </div>
      </nav>
      <div class="hero__title">
        <p class="eyebrow">WEB PUBLISHER · PORTFOLIO</p>
        <h1>최영수</h1>
        <p>금융의 정교함과 커머스의 속도를<br />화면으로 구현해왔습니다.</p>
        <div class="hero__contact">
          <a href="mailto:imaboutthat87@gmail.com">imaboutthat87@gmail.com</a>
          <a href="tel:01051025705">010-5102-5705</a>
        </div>
      </div>
      <a class="scroll-link" href="#projects">Explore projects <span>↓</span></a>
    </header>

    <section class="skills section" id="skills" aria-labelledby="skills-title">
      <div class="section-heading">
        <p class="eyebrow">CORE SKILLS</p>
        <h2 id="skills-title">프로젝트 경험으로<br />쌓아온 기술들입니다.</h2>
      </div>
     
      <div class="skill-static" aria-label="Core skills static view">
        <div v-for="skill in coreSkills" :key="skill.name" class="skill-item">
          <img v-if="skill.icon" :src="skill.icon" :alt="skill.name" />
          <b v-else class="skill-item__mark" aria-hidden="true">{{ skill.mark || skill.name.slice(0, 1) }}</b>
          <span>{{ skill.name }}</span>
        </div>
      </div>
    </section>

    <section class="projects section" id="projects" aria-labelledby="projects-title">
      <div class="section-heading projects__heading">
        <div>
          <p class="eyebrow">PROJECT TIMELINE</p>
          <h2 id="projects-title">프로젝트 이력</h2>
        </div>
        <p class="project-count">{{ filteredProjects.length }} Projects</p>
      </div>

      <nav class="year-filter" aria-label="연도별 프로젝트 보기">
        <button v-for="year in years" :key="year" :class="{ active: selectedYear === year }" @click="selectedYear = year">
          {{ year }}
        </button>
      </nav>

      <div class="timeline">
        <article v-for="project in filteredProjects" :key="`${project.title}-${project.period}`" class="project-card">
          <time :datetime="project.period.slice(0, 7)">{{ project.year }}</time>
          <div class="timeline-dot" aria-hidden="true"></div>
          <div class="project-card__body">
            <p class="project-card__client">{{ project.client }}</p>
            <h3>{{ project.title }}</h3>
            <div class="project-card__meta">
              <span>{{ project.period }}</span>
              <span>{{ project.type }}</span>
            </div>
            <div v-if="project.skills.length" class="project-card__skills" aria-label="차별 기술">
              <span v-for="skill in project.skills" :key="skill">{{ skill }}</span>
            </div>
          </div>
        </article>
      </div>
    </section>

    <footer>
      <p>© {{ new Date().getFullYear() }} YOUNGSOO CHOI</p>
      <a href="#top">Back to top ↑</a>
    </footer>
  </main>
</template>
