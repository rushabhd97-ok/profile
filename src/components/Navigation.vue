<script setup lang="ts">
import { ref } from 'vue'

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

const scrollToSection = (sectionId: string) => {
  closeMenu()
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <nav class="fixed inset-x-0 top-0 z-50 border-b border-white/10 bg-slate-950/70 backdrop-blur-xl">
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
      <div class="flex h-16 items-center justify-between">
        <a href="#" class="flex items-center gap-3 text-sm font-semibold text-ink transition-colors hover:text-success" @click="scrollToSection('hero')">
          <span class="flex h-9 w-9 items-center justify-center rounded-full bg-gradient-to-br from-sky-400 to-fuchsia-500 text-sm font-semibold text-slate-950">R</span>
          <span>Rushabh Dedhia</span>
        </a>

        <div class="hidden items-center gap-2 rounded-full border border-white/10 bg-white/5 p-1.5 md:flex">
          <button @click="scrollToSection('experience')" class="rounded-full px-4 py-2 text-sm font-medium text-ink-soft transition-colors hover:bg-white/10 hover:text-ink">
            Experience
          </button>
          <button @click="scrollToSection('projects')" class="rounded-full px-4 py-2 text-sm font-medium text-ink-soft transition-colors hover:bg-white/10 hover:text-ink">
            Projects
          </button>
          <button @click="scrollToSection('skills')" class="rounded-full px-4 py-2 text-sm font-medium text-ink-soft transition-colors hover:bg-white/10 hover:text-ink">
            Skills
          </button>
          <a href="mailto:rushabh.lucifer@gmail.com" class="rounded-full bg-white/10 px-4 py-2 text-sm font-medium text-white transition-colors hover:bg-white/15">
            Contact
          </a>
        </div>

        <button
          @click="toggleMenu"
          class="rounded-full border border-white/10 bg-white/5 p-2.5 text-ink transition-colors hover:bg-white/10 md:hidden"
          aria-label="Toggle navigation menu"
          :aria-expanded="isMenuOpen"
        >
          <svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>

      <div v-if="isMenuOpen" class="border-t border-white/10 py-4 md:hidden">
        <div class="flex flex-col gap-2">
          <button @click="scrollToSection('experience')" class="rounded-2xl px-3 py-2 text-left text-sm font-medium text-ink-soft transition-colors hover:bg-white/10 hover:text-ink">
            Experience
          </button>
          <button @click="scrollToSection('projects')" class="rounded-2xl px-3 py-2 text-left text-sm font-medium text-ink-soft transition-colors hover:bg-white/10 hover:text-ink">
            Projects
          </button>
          <button @click="scrollToSection('skills')" class="rounded-2xl px-3 py-2 text-left text-sm font-medium text-ink-soft transition-colors hover:bg-white/10 hover:text-ink">
            Skills
          </button>
          <a href="mailto:rushabh.lucifer@gmail.com" class="mt-2 inline-flex items-center justify-center rounded-full bg-white/10 px-4 py-2 text-sm font-medium text-white">
            Contact
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>
