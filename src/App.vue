<script setup lang="ts">
import Navigation from '@/components/Navigation.vue'
import HeroSection from '@/components/HeroSection.vue'
import ExperienceSection from '@/components/ExperienceSection.vue'
import ProjectsSection from '@/components/ProjectsSection.vue'
import SkillsSection from '@/components/SkillsSection.vue'
import FooterNote from '@/components/FooterNote.vue'

const experiences = [
  {
    id: 1,
    company: 'PRPM - OneKirana',
    position: 'Software Developer',
    period: 'March 2026 – June 2026',
    description: 'Architecting core UI features for application modules serving Kirana stores.',
    highlights: [
      'Architected core product modules with React and Next.js for a faster, calmer operator experience.',
      'Collaborated on AWS Lambda workflows and CI/CD delivery pipelines to keep releases dependable.',
      'Added component-level testing and resilient UI patterns to reduce regressions across releases.',
      'Built supporting APIs with NestJS for asynchronous workflows and reliable data handling.',
    ],
    technologies: ['React', 'Next.js', 'NestJS', 'Jest', 'AWS Lambda', 'TypeScript'],
  },
  {
    id: 2,
    company: 'Swegon Bluebox Pvt. Ltd.',
    position: 'Team Lead Web Developer',
    period: 'January 2022 – February 2026',
    description: 'Led a distributed frontend team building industrial web applications with a strong performance focus.',
    highlights: [
      'Led a cross-functional team across India and Italy to ship polished industrial interfaces.',
      'Migrated legacy Angular systems toward Vue/Nuxt and React/Next.js without sacrificing reliability.',
      'Modernized the frontend stack to Vue 3 and Pinia to improve maintainability and clarity.',
      'Built optimized interfaces for memory-constrained IoT workflows and introduced GitHub Actions automation.',
    ],
    technologies: ['Vue.js', 'Nuxt.js', 'React', 'Next.js', 'Pinia', 'CI/CD', 'TypeScript'],
  },
  {
    id: 3,
    company: 'CodeArray Technologies',
    position: 'Associate Software Engineer',
    period: 'August 2019 – August 2021',
    description: 'Built data-rich interfaces for an AI-driven retail intelligence platform with clear visual storytelling.',
    highlights: [
      'Created retail clustering and assortment views with Vue 2 and rich interactive charts.',
      'Partnered closely with product and UX teams to turn complex workflows into simple experiences.',
      'Integrated maps and analytics dashboards to make insight exploration feel fast and intuitive.',
      'Improved debugging and performance through thoughtful tooling and browser-based profiling.',
    ],
    technologies: ['Vue.js', 'Vuex', 'Plotly', 'D3.js', 'Google Maps API', 'JavaScript'],
  },
]

const projects = [
  {
    id: 1,
    title: 'Enterprise HVAC Control System',
    description: 'Modernized an industrial control platform with a calmer, faster interface for operators and technicians.',
    tags: ['Vue.js', 'Nuxt.js', 'amCharts', 'IoT', 'Real-time'],
    highlights: [
      'Lifted perceived performance through focused UI migration and chart optimization.',
      'Delivered live telemetry dashboards for real-time monitoring and control.',
      'Enabled a smaller, more resilient frontend footprint for resource-constrained environments.',
    ],
  },
  {
    id: 2,
    title: 'AI Retail Intelligence Platform',
    description: 'Shaped a multi-layer analytics experience that brought complex retail data into a usable flow.',
    tags: ['Vue.js', 'Plotly', 'D3.js', 'Data Viz', 'REST API'],
    highlights: [
      'Built rich clustering and assortment visualizations for commercial planning.',
      'Made data exploration more flexible through sorting, filtering, and custom components.',
      'Integrated maps and dashboard views to create a more complete story for the user.',
    ],
  },
  {
    id: 3,
    title: 'Next.js Commerce Experience',
    description: 'Delivered a scalable storefront experience with attention to speed, clarity, and maintainability.',
    tags: ['Next.js', 'React', 'TypeScript', 'Tailwind CSS', 'AWS'],
    highlights: [
      'Created an extensible component system for fast feature delivery.',
      'Optimized the app experience around Core Web Vitals and efficient rendering.',
      'Supported reliable deployment with automated pipelines and modern tooling.',
    ],
  },
  {
    id: 4,
    title: 'Real-time IoT Dashboard',
    description: 'Built an interface for streaming operational data that stayed responsive under pressure.',
    tags: ['React', 'WebSockets', 'Highcharts', 'Responsive', 'Performance'],
    highlights: [
      'Handled dense telemetry updates while keeping the interface calm and readable.',
      'Reduced load time significantly through thoughtful component splitting and optimization.',
      'Created responsive layouts that performed well on low-powered hardware.',
    ],
  },
]
</script>

<template>
  <div class="min-h-screen bg-canvas-soft text-ink">
    <Navigation />

    <main>
      <HeroSection />
      <ExperienceSection :experiences="experiences" />
      <ProjectsSection :projects="projects" />
      <SkillsSection />
      <FooterNote />
    </main>
  </div>
</template>

<style scoped>
main {
  position: relative;
  z-index: 1;
}
</style>
