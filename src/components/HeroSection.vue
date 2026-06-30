<script setup lang="ts">
import { ref, onMounted } from 'vue'

const isVisible = ref(false)
const highlights = ['Product-minded frontend engineering', 'Design systems and interactive UI', 'Performance-first delivery']

onMounted(() => {
  isVisible.value = true
})
</script>

<template>
  <section id="hero" class="relative overflow-hidden px-4 pb-24 pt-28 sm:px-6 lg:px-8 lg:pt-36">
    <div class="absolute inset-0 bg-[radial-gradient(circle_at_top_left,_rgba(96,165,250,0.16),_transparent_36%),radial-gradient(circle_at_85%_20%,_rgba(244,114,182,0.16),_transparent_30%),linear-gradient(135deg,_rgba(2,6,23,0.98),_rgba(11,17,32,0.92))]" />
    <div class="absolute inset-x-0 top-0 h-[440px] bg-[linear-gradient(120deg,_rgba(96,165,250,0.22),_rgba(45,212,191,0.18),_rgba(167,139,250,0.16),_rgba(244,114,182,0.15))] blur-3xl" />

    <div class="relative mx-auto max-w-7xl">
      <div class="grid gap-10 lg:grid-cols-[1.05fr_0.95fr] lg:items-center">
        <div class="max-w-3xl">
          <div class="inline-flex items-center gap-2 rounded-full border border-white/10 bg-white/8 px-3 py-2 text-sm text-ink-soft shadow-[0_8px_24px_rgba(2,6,23,0.25)] backdrop-blur">
            <span class="h-2.5 w-2.5 rounded-full bg-success" />
            Available for product-focused frontend work
          </div>

          <h1 class="mt-6 text-balance font-display-xl text-ink">
            Building calm, high-performing interfaces for modern products.
          </h1>

          <p class="mt-6 max-w-2xl text-lg leading-8 text-ink-soft sm:text-xl">
            I’m Rushabh, a frontend engineer with 6+ years of experience crafting Vue, React, and Next.js experiences that feel sharp, intuitive, and easy to trust.
          </p>

          <div class="mt-8 flex flex-col gap-3 sm:flex-row">
            <a href="mailto:rushabh.lucifer@gmail.com" class="btn-primary">
              Start a conversation
            </a>
            <a href="https://linkedin.com/in/rushabh-dedhia-ab108314b/" target="_blank" rel="noopener noreferrer" class="btn-secondary">
              View LinkedIn
            </a>
          </div>

          <div class="mt-8 flex flex-wrap gap-3">
            <div v-for="item in highlights" :key="item" class="rounded-full border border-white/10 bg-white/8 px-3 py-2 text-sm text-ink-soft shadow-[0_6px_16px_rgba(2,6,23,0.2)] backdrop-blur">
              {{ item }}
            </div>
          </div>
        </div>

        <div class="relative">
          <div class="rounded-[2rem] border border-white/10 bg-slate-950/70 p-5 shadow-[0_20px_60px_rgba(2,6,23,0.4)] backdrop-blur-xl">
            <div class="rounded-[1.5rem] border border-white/10 bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900 p-5 text-white">
              <div class="flex items-center justify-between">
                <div>
                  <p class="font-caption-mono text-white/70">Current focus</p>
                  <p class="mt-1 text-lg font-semibold">Frontend systems & product delivery</p>
                </div>
                <span class="rounded-full border border-cyan-400/20 bg-cyan-400/10 px-3 py-1 text-xs font-medium text-cyan-200">
                  Available now
                </span>
              </div>

              <div class="mt-6 rounded-[1.25rem] border border-white/10 bg-white/8 p-4">
                <div class="flex items-center justify-between text-sm text-white/70">
                  <span>Core stack</span>
                  <span class="font-caption-mono">modern web</span>
                </div>
                <div class="mt-3 flex flex-wrap gap-2">
                  <span class="rounded-full border border-white/10 bg-white/10 px-3 py-1 text-sm text-white">Vue 3</span>
                  <span class="rounded-full border border-white/10 bg-white/10 px-3 py-1 text-sm text-white">React</span>
                  <span class="rounded-full border border-white/10 bg-white/10 px-3 py-1 text-sm text-white">Next.js</span>
                  <span class="rounded-full border border-white/10 bg-white/10 px-3 py-1 text-sm text-white">TypeScript</span>
                </div>
              </div>
            </div>

            <div class="mt-4 grid gap-3 sm:grid-cols-2">
              <div class="rounded-[1.25rem] border border-white/10 bg-white/8 p-4">
                <p class="font-caption-mono text-success">Delivery</p>
                <p class="mt-2 text-2xl font-semibold text-ink">6+ years</p>
                <p class="mt-1 text-sm text-ink-soft">Designing and shipping polished interfaces</p>
              </div>
              <div class="rounded-[1.25rem] border border-white/10 bg-white/8 p-4">
                <p class="font-caption-mono text-success">Impact</p>
                <p class="mt-2 text-2xl font-semibold text-ink">50+ launches</p>
                <p class="mt-1 text-sm text-ink-soft">Across web platforms, dashboards, and commerce</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.animate-in {
  opacity: 1;
  transform: translateY(0);
}
</style>
