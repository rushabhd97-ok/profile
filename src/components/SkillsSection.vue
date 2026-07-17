<script setup lang="ts">
import SectionHeading from '@/components/SectionHeading.vue'

interface Skill {
  category: string
  items: string[]
}

const skills: Skill[] = [
  {
    category: 'Frontend Frameworks',
    items: ['React', 'Next.js', 'Vue.js 2/3', 'Nuxt.js', 'Angular 2', 'Vite'],
  },
  {
    category: 'Languages & Core',
    items: ['JavaScript (ES6+)', 'TypeScript', 'HTML5', 'CSS3', 'Sass', 'CSS architecture'],
  },
  {
    category: 'Data Visualization',
    items: ['D3.js', 'Plotly', 'Highcharts', 'amCharts', 'Google Maps API', 'Canvas API'],
  },
  {
    category: 'Testing & DevOps',
    items: ['Jest', 'React Testing Library', 'Chrome DevTools', 'Git', 'CI/CD', 'AWS Lambda'],
  },
  {
    category: 'Backend & Databases',
    items: ['NestJS', 'REST APIs', 'GraphQL', 'PostgreSQL', 'MongoDB', 'Firebase'],
  },
  {
    category: 'Tools & Platforms',
    items: ['Webpack', 'ESLint', 'Prettier', 'Figma', 'Bitbucket', 'Jira', 'Notion'],
  },
]
</script>

<template>
  <section id="skills" class="section">
    <div class="container">
      <SectionHeading
        eyebrow="Core competencies"
        title="Modern tooling, thoughtful systems, and product-minded execution."
        description="I bring a pragmatic mix of UI craft, engineering discipline, and collaboration to teams that care about quality and momentum."
      />

      <div class="skill-grid row g-3">
        <div v-for="skillGroup in skills" :key="skillGroup.category" class="col-12 col-md-6 col-lg-4">
          <div class="skill-card card h-100 m-0">
            <h3>{{ skillGroup.category }}</h3>
            <div class="skill-card__items">
              <span v-for="skill in skillGroup.items" :key="skill">{{ skill }}</span>
            </div>
          </div>
        </div>
      </div>

      <div class="stats-grid row g-3 mt-4">
        <div class="col-12 col-sm-6 col-lg-3">
          <div class="stat-card card card--soft h-100 m-0">
            <p>6+</p>
            <span>Years of experience</span>
          </div>
        </div>
        <div class="col-12 col-sm-6 col-lg-3">
          <div class="stat-card card card--soft h-100 m-0">
            <p>10+</p>
            <span>Major projects shipped</span>
          </div>
        </div>
        <div class="col-12 col-sm-6 col-lg-3">
          <div class="stat-card card card--soft h-100 m-0">
            <p>3</p>
            <span>Teams led</span>
          </div>
        </div>
        <div class="col-12 col-sm-6 col-lg-3">
          <div class="stat-card card card--soft h-100 m-0">
            <p>15+</p>
            <span>Technologies used</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>


.skill-card {
  padding: 1.35rem;
}

.skill-card h3 {
  margin: 0;
  font-size: 1.08rem;
}

.skill-card__items {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-top: 1rem;
}

.skill-card__items span {
  padding: 0.45rem 0.7rem;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(255, 255, 255, 0.05);
  color: var(--text-soft);
  font-size: 0.9rem;
}



.stat-card {
  padding: 1.2rem;
  text-align: center;
}

.stat-card p {
  margin: 0;
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--text);
}

.stat-card span {
  display: inline-block;
  margin-top: 0.35rem;
  color: var(--text-soft);
}


</style>
