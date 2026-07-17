<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue'
import ContactModal from './ContactModal.vue'

const isMenuOpen = ref(false)
const isContactModalOpen = ref(false)
const activeSection = ref('hero')
const sections = ['hero', 'experience', 'projects', 'skills']

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

const openContactModal = () => {
  closeMenu()
  isContactModalOpen.value = true
}

const downloadResume = (fileName = 'Rushabh Dedhia - New Resume.pdf') => {
  closeMenu()

  const resolvedFileName =
    fileName.toLowerCase() === 'resume.pdf'
      ? 'Rushabh Dedhia - New Resume.pdf'
      : fileName

  const link = document.createElement('a')
  link.href = `${import.meta.env.BASE_URL}${encodeURIComponent(resolvedFileName)}`
  link.download = resolvedFileName
  document.body.appendChild(link)
  link.click()
  document.body.removeChild(link)
}

const scrollToSection = (sectionId: string) => {
  closeMenu()
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const updateActiveSection = () => {
  const scrollPosition = window.scrollY + 140

  for (const sectionId of sections) {
    const element = document.getElementById(sectionId)

    if (!element) {
      continue
    }

    const top = element.offsetTop
    const bottom = top + element.offsetHeight

    if (scrollPosition >= top && scrollPosition < bottom) {
      activeSection.value = sectionId
      break
    }
  }
}

onMounted(() => {
  updateActiveSection()
  window.addEventListener('scroll', updateActiveSection, { passive: true })
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', updateActiveSection)
})
</script>

<template>
  <nav class="topbar">
    <div class="container topbar__inner">
      <a href="#" class="brand" @click="scrollToSection('hero')">
        <span class="brand__mark">R</span>
        <span>Rushabh Dedhia</span>
      </a>

      <div class="topbar__links">
        <button
          @click="scrollToSection('experience')"
          :class="{ 'is-active': activeSection === 'experience' }"
        >
          Experience
        </button>
        <button
          @click="scrollToSection('projects')"
          :class="{ 'is-active': activeSection === 'projects' }"
        >
          Projects
        </button>
        <button
          @click="scrollToSection('skills')"
          :class="{ 'is-active': activeSection === 'skills' }"
        >
          Skills
        </button>
        <button @click="downloadResume('resume.pdf')">Resume</button>
        <button type="button" @click="openContactModal">Contact</button>
      </div>

      <button
        @click="toggleMenu"
        class="mobile-toggle"
        aria-label="Toggle navigation menu"
        :aria-expanded="isMenuOpen"
      >
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
          <path v-if="!isMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>

    <div v-if="isMenuOpen" class="mobile-menu">
      <button @click="scrollToSection('experience')">Experience</button>
      <button @click="scrollToSection('projects')">Projects</button>
      <button @click="scrollToSection('skills')">Skills</button>
      <button type="button" @click="openContactModal">Contact</button>
    </div>
  </nav>

  <ContactModal v-model="isContactModalOpen" />
</template>

<style scoped>
.topbar {
  position: fixed;
  inset: 0 0 auto 0;
  z-index: 50;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(5, 8, 22, 0.75);
  backdrop-filter: blur(18px);
}

.topbar__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  min-height: 4rem;
  padding: 0 1.25rem;
}

.brand {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 0.95rem;
  font-weight: 700;
  color: var(--text);
}

.brand__mark {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2.3rem;
  height: 2.3rem;
  border-radius: 999px;
  background: linear-gradient(135deg, var(--accent), var(--accent-strong));
  color: #040816;
  font-weight: 700;
}

.topbar__links {
  display: none;
  align-items: center;
  gap: 0.35rem;
  border-radius: 999px;
  padding: 0.35rem;
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(255, 255, 255, 0.05);
}

.topbar__links button,
.topbar__links a,
.mobile-menu button,
.mobile-menu a {
  border: 0;
  background: transparent;
  color: var(--text-soft);
  font: inherit;
  padding: 0.6rem 0.95rem;
  border-radius: 999px;
  cursor: pointer;
}

.topbar__links button:hover,
.mobile-menu button:hover {
  background: rgba(255, 255, 255, 0.08);
  color: var(--text);
}

.topbar__links button.is-active,
.mobile-menu button.is-active {
  background: rgba(0, 112, 243, 0.18);
  color: var(--text);
}

.mobile-toggle {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2.5rem;
  height: 2.5rem;
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.05);
  color: var(--text);
  cursor: pointer;
}

.mobile-toggle svg {
  width: 1.15rem;
  height: 1.15rem;
}

.mobile-menu {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  padding: 0.75rem 1.25rem 1rem;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
}

@media (min-width: 768px) {
  .topbar__links {
    display: inline-flex;
  }

  .mobile-toggle,
  .mobile-menu {
    display: none;
  }
}
</style>
