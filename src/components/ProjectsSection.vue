<script setup lang="ts">
import { computed } from 'vue'

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
  <section id="projects" class="px-4 py-24 sm:px-6 lg:px-8">
    <div class="mx-auto max-w-7xl">
      <div class="mb-12 max-w-2xl">
        <p class="font-caption-mono text-success mb-3">Selected work</p>
        <h2 class="text-3xl font-semibold tracking-[-0.02em] text-ink sm:text-4xl">
          Product-focused builds that balance clarity and ambition.
        </h2>
      </div>

      <div class="space-y-10">
        <div v-for="(projects, year) in projectsByYear" :key="year">
          <div class="mb-6 flex items-center gap-3">
            <h3 class="text-sm font-semibold uppercase tracking-[0.2em] text-ink-soft">{{ year }}</h3>
            <div class="h-px flex-1 bg-hairline" />
          </div>

          <div class="grid gap-6 lg:grid-cols-2">
            <article v-for="project in projects" :key="project.id" class="rounded-[1.75rem] border border-hairline bg-white/90 p-7 shadow-[0_16px_40px_rgba(23,23,23,0.05)] transition-transform duration-200 hover:-translate-y-1">
              <div class="flex items-center justify-between gap-3">
                <h4 class="text-xl font-semibold text-ink">{{ project.title }}</h4>
                <span class="rounded-full border border-hairline bg-canvas-soft px-3 py-1 text-xs font-medium uppercase tracking-[0.2em] text-ink-soft">
                  Case study
                </span>
              </div>

              <p class="mt-4 text-base leading-8 text-ink-soft">{{ project.description }}</p>

              <div v-if="project.highlights.length > 0" class="mt-6">
                <ul class="space-y-2.5">
                  <li v-for="(highlight, idx) in project.highlights" :key="idx" class="flex gap-3 text-sm leading-7 text-ink-soft">
                    <span class="mt-1.5 h-2 w-2 flex-shrink-0 rounded-full bg-success" />
                    <span>{{ highlight }}</span>
                  </li>
                </ul>
              </div>

              <div class="mt-6 flex flex-wrap gap-2">
                <span v-for="tag in project.tags" :key="tag" class="rounded-full border border-hairline bg-canvas-soft px-3 py-1.5 text-xs font-medium text-ink">
                  {{ tag }}
                </span>
              </div>

              <a v-if="project.link" :href="project.link" target="_blank" rel="noopener noreferrer" class="mt-6 inline-flex items-center text-sm font-semibold text-success transition-colors hover:text-success-deep">
                View project
                <span class="ml-2">→</span>
              </a>
            </article>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
