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
        <p class="font-caption-mono mb-3 text-success">Selected work</p>
        <h2 class="section-title">
          Product-focused builds that balance clarity and ambition.
        </h2>
      </div>

      <div class="space-y-10">
        <div v-for="(projects, year) in projectsByYear" :key="year">
          <div class="mb-6 flex items-center gap-3">
            <h3 class="text-sm font-semibold uppercase tracking-[0.2em] text-ink-soft">{{ year }}</h3>
            <div class="h-px flex-1 bg-white/10" />
          </div>

          <div class="grid gap-6 lg:grid-cols-2">
            <article v-for="project in projects" :key="project.id" class="group card overflow-hidden">
              <div class="h-40 rounded-[1.25rem] border border-white/10 bg-gradient-to-br from-sky-500/30 via-cyan-400/20 to-fuchsia-500/25 p-4">
                <div class="flex h-full items-end justify-between rounded-[1rem] border border-white/10 bg-slate-950/60 p-4">
                  <div>
                    <p class="font-caption-mono text-cyan-200">Featured build</p>
                    <p class="mt-2 text-sm font-medium text-white">{{ project.title }}</p>
                  </div>
                  <div class="h-10 w-10 rounded-full border border-cyan-400/20 bg-cyan-400/10" />
                </div>
              </div>

              <div class="mt-6 flex items-center justify-between gap-3">
                <h4 class="text-xl font-semibold text-ink">{{ project.title }}</h4>
                <span class="rounded-full border border-white/10 bg-white/8 px-3 py-1 text-xs font-medium uppercase tracking-[0.2em] text-ink-soft">
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
                <span v-for="tag in project.tags" :key="tag" class="rounded-full border border-white/10 bg-white/8 px-3 py-1.5 text-xs font-medium text-ink-soft">
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
