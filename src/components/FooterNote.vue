<script setup lang="ts">
defineProps<{
  title?: string
  description?: string
}>()
</script>

<template>
  <footer class="bg-ink px-4 py-16 text-white sm:px-6 lg:px-8">
    <div class="mx-auto max-w-7xl">
      <div class="grid gap-10 rounded-[2rem] border border-white/10 bg-white/5 p-8 sm:p-10 lg:grid-cols-[1.2fr_0.8fr_0.8fr_0.8fr]">
        <div>
          <p class="font-caption-mono text-white/70">Available for new opportunities</p>
          <h3 class="mt-3 text-2xl font-semibold text-white">Let’s build something polished and lasting.</h3>
          <p class="mt-4 max-w-md text-sm leading-7 text-white/70">
            I enjoy working on products where product thinking, polished UI, and reliable engineering all matter.
          </p>
        </div>

        <div>
          <h4 class="text-sm font-semibold uppercase tracking-[0.2em] text-white/70">Connect</h4>
          <ul class="mt-4 space-y-3 text-sm text-white/80">
            <li><a href="https://linkedin.com/in/rushabh-dedhia-ab108314b/" target="_blank" rel="noopener noreferrer" class="transition-colors hover:text-white">LinkedIn</a></li>
            <li><a href="https://github.com" target="_blank" rel="noopener noreferrer" class="transition-colors hover:text-white">GitHub</a></li>
            <li><a href="mailto:rushabh.lucifer@gmail.com" class="transition-colors hover:text-white">Email</a></li>
          </ul>
        </div>

        <div>
          <h4 class="text-sm font-semibold uppercase tracking-[0.2em] text-white/70">Experience</h4>
          <ul class="mt-4 space-y-3 text-sm text-white/80">
            <li>PRPM - OneKirana</li>
            <li>Swegon Bluebox</li>
            <li>CodeArray Technologies</li>
          </ul>
        </div>

        <div>
          <h4 class="text-sm font-semibold uppercase tracking-[0.2em] text-white/70">Stack</h4>
          <ul class="mt-4 space-y-3 text-sm text-white/80">
            <li>React / Next.js</li>
            <li>Vue / Nuxt</li>
            <li>TypeScript / Tailwind</li>
          </ul>
        </div>
      </div>

      <div class="mt-8 flex flex-col gap-3 border-t border-white/10 pt-6 text-sm text-white/60 sm:flex-row sm:items-center sm:justify-between">
        <p>© 2026 Rushabh Dedhia. Crafted with care.</p>
        <a href="/resume.pdf" class="transition-colors hover:text-white">Download resume</a>
      </div>
    </div>
  </footer>
</template>
