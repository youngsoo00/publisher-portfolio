<script setup>
import { computed, onMounted, ref } from 'vue'
import { coreSkills, projects } from './data/projects'

const selectedYear = ref('All')
const years = ['All', ...new Set(projects.map((project) => project.year))]
const loopSkills = [...coreSkills, ...coreSkills]
const skillByName = Object.fromEntries(coreSkills.map((skill) => [skill.name, skill]))
const primarySkills = [
  ['Vue', 'Progressive JavaScript Framework'],
  ['JavaScript', 'Dynamic & Interactive Web'],
  ['HTML5 / CSS3', 'Modern Web Standards'],
  ['SCSS', 'Maintainable Stylesheets'],
  ['jQuery', 'Dynamic UI Foundation']
].map(([name, description]) => ({ ...skillByName[name], description }))
const frameworkSkills = ['Vuetify', 'Bootstrap', 'PrimeVue', 'WebSquare'].map((name) => skillByName[name])
const collaborationSkills = ['Git', 'Figma', 'Zeplin', 'Adobe XD', 'Photoshop', 'PUG'].map((name) => skillByName[name])
const filteredProjects = computed(() => selectedYear.value === 'All'
  ? projects
  : projects.filter((project) => project.year === selectedYear.value))

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible')
        observer.unobserve(entry.target)
      }
    })
  }, { threshold: 0, rootMargin: '0px 0px -8% 0px' })

  document.querySelectorAll('.reveal').forEach((item) => observer.observe(item))
})
</script>

<template>
  <main>
    <header class="hero" id="top">
      <nav class="hero__nav hero-reveal hero-reveal--one" aria-label="주요 메뉴">
        <a class="brand" href="#top"></a>
        <div>
          <a href="#skills">About</a>
          <a href="#projects">Project</a>
          <a href="mailto:imaboutthat87@gmail.com">Contact</a>
        </div>
      </nav>
      <div class="hero__title hero-reveal hero-reveal--two">
        <p class="eyebrow">WEB PUBLISHER · PORTFOLIO</p>
        <h1>최영수</h1>
        <p>복잡한 요구사항을<br />정교한 화면으로 구현합니다.</p>
        <div class="hero__contact">
          <a href="mailto:imaboutthat87@gmail.com">imaboutthat87@gmail.com</a>
          <a href="tel:01051025705">010-5102-5705</a>
        </div>
      </div>
      <aside class="hero__metrics hero-reveal hero-reveal--two" aria-label="경력 요약">
        <div class="hero__metric">
          <strong>13<span>+</span></strong>
          <b>YEARS</b>
          <p>경험이 만드는<br />더 나은 웹 경험</p>
        </div>
        <div class="hero__metric">
          <strong>35</strong>
          <b>PROJECTS</b>
          <p>다양한 산업의<br />프로젝트 경험</p>
        </div>
      </aside>
      <div class="hero__art" aria-hidden="true"><span></span><i></i></div>
      <a class="scroll-link hero-reveal hero-reveal--three" href="#projects">Explore projects <span>↓</span></a>
    </header>

    <section class="skills section" id="skills" aria-labelledby="skills-title">
      <div class="skills__intro reveal">
        <div class="section-heading">
          <p class="eyebrow">CORE SKILLS</p>
          <h2 id="skills-title">프로젝트 경험으로<br />쌓아온 기술들입니다.</h2>
        </div>
        <div class="skills__summary">
          <p>다양한 프로젝트 경험을 통해 축적한 기술로<br />사용자 중심의 웹을 만듭니다.</p>
          <span>SKILLS<br />MAKE<br />IDEAS<br />REAL</span>
        </div>
      </div>
      <div class="skills__group skills__group--primary reveal">
        <div class="skills__group-heading">
          <p>PRIMARY SKILLS</p>
          <span>핵심 기술과 구현 역량</span>
        </div>
        <div class="primary-skill-grid">
          <article v-for="skill in primarySkills" :key="skill.name" class="primary-skill-card">
            <img v-if="skill.icon" :src="skill.icon" :alt="skill.name" />
            <b v-else class="skill-item__mark" aria-hidden="true">{{ skill.mark || skill.name.slice(0, 1) }}</b>
            <h3>{{ skill.name }}</h3>
            <p>{{ skill.description }}</p>
          </article>
        </div>
      </div>
      <div class="skills__minor-groups reveal">
        <div class="skills__group">
          <div class="skills__group-heading">
            <p>FRAMEWORK / UI</p>
            <span>더 나은 개발을 위한 UI 라이브러리</span>
          </div>
          <div class="minor-skill-grid">
            <article v-for="skill in frameworkSkills" :key="skill.name" class="minor-skill-card">
              <img v-if="skill.icon" :src="skill.icon" :alt="skill.name" />
              <b v-else class="skill-item__mark" aria-hidden="true">{{ skill.mark || skill.name.slice(0, 1) }}</b>
              <span>{{ skill.name }}</span>
            </article>
          </div>
        </div>
        <div class="skills__group">
          <div class="skills__group-heading">
            <p>DESIGN / COLLABORATION</p>
            <span>효율적인 협업과 완성도를 위한 도구</span>
          </div>
          <div class="minor-skill-grid">
            <article v-for="skill in collaborationSkills" :key="skill.name" class="minor-skill-card">
              <img v-if="skill.icon" :src="skill.icon" :alt="skill.name" />
              <b v-else class="skill-item__mark" aria-hidden="true">{{ skill.mark || skill.name.slice(0, 1) }}</b>
              <span>{{ skill.name }}</span>
            </article>
          </div>
        </div>
      </div>
    </section>

    <section class="projects section" id="projects" aria-labelledby="projects-title">
      <div class="section-heading projects__heading reveal">
        <div>
          <p class="eyebrow">PROJECT TIMELINE</p>
          <h2 id="projects-title">프로젝트 이력</h2>
        </div>
        <p class="project-count">{{ filteredProjects.length }} Projects</p>
      </div>

      <nav class="year-filter reveal" aria-label="연도별 프로젝트 보기">
        <button v-for="year in years" :key="year" :class="{ active: selectedYear === year }" @click="selectedYear = year">
          {{ year }}
        </button>
      </nav>

      <div class="timeline reveal">
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
