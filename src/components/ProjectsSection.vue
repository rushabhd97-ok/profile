<script setup lang="ts">
import { computed } from 'vue'
import SectionHeading from '@/components/SectionHeading.vue'

interface Project {
  id: number
  title: string
  description: string
  tags: string[]
  link?: string
  highlights: string[]
}

const props = defineProps<{
  projects: Project[]
}>()

const projectsByYear = computed(() => {
  const grouped: { [key: string]: Project[] } = {}
  props.projects.forEach(project => {
    const year = '2024-2026'
    if (!grouped[year]) {
      grouped[year] = []
    }
    grouped[year].push(project)
  })
  return grouped
})
</script>

<template>
  <section id="projects" class="section">
    <div class="container">
      <SectionHeading
        eyebrow="Selected work"
        title="Product-focused builds that balance clarity and ambition."
      />

      <div class="project-groups">
        <div v-for="(projects, year) in projectsByYear" :key="year" class="project-group">
          <div class="project-group__header">
            <h3>{{ year }}</h3>
            <div class="project-group__line" />
          </div>

          <div class="project-grid">
            <article v-for="project in projects" :key="project.id" class="project-card card">
              <div class="project-card__visual">
                <div class="project-card__visual-inner">
                  <p>Featured build</p>
                  <p>{{ project.title }}</p>
                </div>
              </div>

              <div class="project-card__body">
                <div class="project-card__title-row">
                  <h4>{{ project.title }}</h4>
                  <span>Case study</span>
                </div>

                <p class="project-card__description">{{ project.description }}</p>

                <div v-if="project.highlights.length > 0" class="project-card__list">
                  <ul>
                    <li v-for="(highlight, idx) in project.highlights" :key="idx">
                      <span class="project-card__bullet" />
                      <span>{{ highlight }}</span>
                    </li>
                  </ul>
                </div>

                <div class="project-card__tags">
                  <span v-for="tag in project.tags" :key="tag">{{ tag }}</span>
                </div>

                <a v-if="project.link" :href="project.link" target="_blank" rel="noopener noreferrer">
                  View project
                  <span>→</span>
                </a>
              </div>
            </article>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.project-groups {
  display: grid;
  gap: 2rem;
}

.project-group__header {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  margin-bottom: 1rem;
}

.project-group__header h3 {
  font-size: 0.82rem;
  letter-spacing: 0.24em;
  text-transform: uppercase;
  color: var(--text-muted);
}

.project-group__line {
  flex: 1;
  height: 1px;
  background: rgba(255, 255, 255, 0.12);
}

.project-grid {
  display: grid;
  gap: 1rem;
}

.project-card {
  overflow: hidden;
}

.project-card__visual {
  padding: 1rem;
  background: linear-gradient(135deg, rgba(96, 165, 250, 0.28), rgba(217, 70, 239, 0.2));
}

.project-card__visual-inner {
  display: flex;
  align-items: end;
  justify-content: space-between;
  gap: 1rem;
  min-height: 10rem;
  padding: 1rem;
  border-radius: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(4, 8, 22, 0.72);
}

.project-card__visual-inner p:first-child {
  margin: 0;
  color: #bae6fd;
  font-size: 0.82rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
}

.project-card__visual-inner p:last-child {
  margin: 0.35rem 0 0;
  color: var(--text);
  font-weight: 600;
}

.project-card__body {
  padding: 1.25rem;
}

.project-card__title-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.75rem;
}

.project-card__title-row h4 {
  margin: 0;
  font-size: 1.1rem;
}

.project-card__title-row span {
  padding: 0.4rem 0.65rem;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  font-size: 0.74rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--text-muted);
}

.project-card__description {
  margin-top: 1rem;
  line-height: 1.75;
}

.project-card__list {
  margin-top: 1rem;
}

.project-card__list ul {
  list-style: none;
  display: grid;
  gap: 0.65rem;
}

.project-card__list li {
  display: flex;
  gap: 0.7rem;
  align-items: flex-start;
  color: var(--text-soft);
  line-height: 1.7;
}

.project-card__bullet {
  display: inline-block;
  width: 0.55rem;
  height: 0.55rem;
  border-radius: 999px;
  background: var(--success);
  margin-top: 0.45rem;
  flex-shrink: 0;
}

.project-card__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-top: 1rem;
}

.project-card__tags span {
  padding: 0.45rem 0.7rem;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(255, 255, 255, 0.05);
  color: var(--text-soft);
  font-size: 0.85rem;
}

.project-card a {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  margin-top: 1rem;
  color: var(--success);
  font-weight: 600;
}

@media (min-width: 900px) {
  .project-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
</style>
