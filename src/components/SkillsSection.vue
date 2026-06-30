<script setup lang="ts">
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
    items: ['JavaScript (ES6+)', 'TypeScript', 'HTML5', 'CSS3', 'Sass', 'Tailwind CSS'],
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
  <section id="skills" class="px-4 py-24 sm:px-6 lg:px-8">
    <div class="mx-auto max-w-7xl">
      <div class="mb-12 max-w-2xl">
        <p class="font-caption-mono mb-3 text-success">Core competencies</p>
        <h2 class="section-title">
          Modern tooling, thoughtful systems, and product-minded execution.
        </h2>
        <p class="section-subtitle mt-4">
          I bring a pragmatic mix of UI craft, engineering discipline, and collaboration to teams that care about quality and momentum.
        </p>
      </div>

      <div class="grid gap-6 md:grid-cols-2 xl:grid-cols-3">
        <div v-for="skillGroup in skills" :key="skillGroup.category" class="card">
          <h3 class="text-lg font-semibold text-ink">{{ skillGroup.category }}</h3>
          <div class="mt-5 flex flex-wrap gap-2">
            <span v-for="skill in skillGroup.items" :key="skill" class="rounded-full border border-white/10 bg-white/8 px-3 py-1.5 text-sm font-medium text-ink-soft">
              {{ skill }}
            </span>
          </div>
        </div>
      </div>

      <div class="mt-10 grid gap-4 md:grid-cols-2 xl:grid-cols-4">
        <div class="rounded-[1.25rem] border border-white/10 bg-white/8 p-5 text-center shadow-[0_10px_24px_rgba(2,6,23,0.25)]">
          <p class="text-3xl font-semibold text-ink">6+</p>
          <p class="mt-2 text-sm text-ink-soft">Years of experience</p>
        </div>
        <div class="rounded-[1.25rem] border border-white/10 bg-white/8 p-5 text-center shadow-[0_10px_24px_rgba(2,6,23,0.25)]">
          <p class="text-3xl font-semibold text-ink">10+</p>
          <p class="mt-2 text-sm text-ink-soft">Major projects shipped</p>
        </div>
        <div class="rounded-[1.25rem] border border-white/10 bg-white/8 p-5 text-center shadow-[0_10px_24px_rgba(2,6,23,0.25)]">
          <p class="text-3xl font-semibold text-ink">3</p>
          <p class="mt-2 text-sm text-ink-soft">Teams led</p>
        </div>
        <div class="rounded-[1.25rem] border border-white/10 bg-white/8 p-5 text-center shadow-[0_10px_24px_rgba(2,6,23,0.25)]">
          <p class="text-3xl font-semibold text-ink">15+</p>
          <p class="mt-2 text-sm text-ink-soft">Technologies used</p>
        </div>
      </div>
    </div>
  </section>
</template>
