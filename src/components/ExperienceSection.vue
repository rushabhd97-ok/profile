<script setup lang="ts">
interface ExperienceItem {
  id: number
  company: string
  position: string
  period: string
  description: string
  highlights: string[]
  technologies: string[]
}

defineProps<{
  experiences: ExperienceItem[]
}>()
</script>

<template>
  <section id="experience" class="px-4 py-24 sm:px-6 lg:px-8">
    <div class="mx-auto max-w-7xl">
      <div class="mb-12 max-w-2xl">
        <p class="font-caption-mono mb-3 text-success">Career path</p>
        <h2 class="section-title">
          Experience shaping thoughtful product interfaces.
        </h2>
        <p class="section-subtitle mt-4">
          My work has centered on turning complex product needs into elegant, reliable user experiences that feel calm and effortless.
        </p>
      </div>

      <div class="space-y-5">
        <div v-for="(exp, index) in experiences" :key="exp.id" class="relative">
          <div v-if="index < experiences.length - 1" class="absolute left-6 top-16 bottom-[-1.25rem] w-px bg-white/10" />

          <div class="flex gap-5">
            <div class="flex flex-col items-center pt-1">
              <div class="flex h-12 w-12 items-center justify-center rounded-full bg-gradient-to-br from-sky-400 to-fuchsia-500 text-sm font-semibold text-slate-950 shadow-[0_10px_24px_rgba(34,211,238,0.24)]">
                {{ index + 1 }}
              </div>
            </div>

            <div class="flex-1 pb-2">
              <div class="card">
                <div class="flex flex-col gap-3 md:flex-row md:items-start md:justify-between">
                  <div>
                    <h3 class="text-xl font-semibold text-ink">{{ exp.position }}</h3>
                    <p class="mt-1 text-base font-medium text-success">{{ exp.company }}</p>
                  </div>
                  <p class="font-caption-mono text-ink-mute">{{ exp.period }}</p>
                </div>

                <p class="mt-5 text-base leading-8 text-ink-soft">{{ exp.description }}</p>

                <div v-if="exp.highlights.length > 0" class="mt-6">
                  <ul class="space-y-3">
                    <li v-for="(highlight, idx) in exp.highlights" :key="idx" class="flex gap-3 text-sm leading-7 text-ink-soft">
                      <span class="mt-1 h-2.5 w-2.5 flex-shrink-0 rounded-full bg-success" />
                      <span>{{ highlight }}</span>
                    </li>
                  </ul>
                </div>

                <div v-if="exp.technologies.length > 0" class="mt-6 flex flex-wrap gap-2">
                  <span v-for="tech in exp.technologies" :key="tech" class="rounded-full border border-white/10 bg-white/8 px-3 py-1.5 text-xs font-medium text-ink-soft">
                    {{ tech }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
