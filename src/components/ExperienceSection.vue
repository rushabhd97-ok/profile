<script setup lang="ts">
import SectionHeading from '@/components/SectionHeading.vue'

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
  <section id="experience" class="section">
    <div class="container">
      <SectionHeading
        eyebrow="Career path"
        title="Experience shaping thoughtful product interfaces."
        description="My work has centered on turning complex product needs into elegant, reliable user experiences that feel calm and effortless."
      />

      <div class="timeline">
        <div v-for="(exp, index) in experiences" :key="exp.id" class="timeline__item">
          <div v-if="index < experiences.length - 1" class="timeline__connector" />

          <div class="timeline__marker">{{ index + 1 }}</div>

          <div class="timeline__card card">
            <div class="timeline__header">
              <div>
                <h3>{{ exp.position }}</h3>
                <p class="timeline__company">{{ exp.company }}</p>
              </div>
              <p class="timeline__period">{{ exp.period }}</p>
            </div>

            <p class="timeline__description">{{ exp.description }}</p>

            <div v-if="exp.highlights.length > 0" class="timeline__list">
              <ul>
                <li v-for="(highlight, idx) in exp.highlights" :key="idx">
                  <span class="timeline__bullet" />
                  <span>{{ highlight }}</span>
                </li>
              </ul>
            </div>

            <div v-if="exp.technologies.length > 0" class="timeline__tags">
              <span v-for="tech in exp.technologies" :key="tech">{{ tech }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.timeline {
  display: grid;
  gap: 1rem;
}

.timeline__item {
  position: relative;
  display: grid;
  grid-template-columns: 3rem minmax(0, 1fr);
  gap: 1rem;
  align-items: start;
}

.timeline__connector {
  position: absolute;
  left: 1.5rem;
  top: 3rem;
  bottom: -1rem;
  width: 1px;
  background: rgba(255, 255, 255, 0.12);
}

.timeline__marker {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 3rem;
  height: 3rem;
  border-radius: 999px;
  background: linear-gradient(135deg, var(--accent), var(--accent-strong));
  color: #040816;
  font-weight: 700;
  box-shadow: 0 14px 32px rgba(96, 165, 250, 0.24);
}

.timeline__card {
  padding: 1.35rem;
}

.timeline__header {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.timeline__header h3 {
  font-size: 1.2rem;
  margin: 0;
}

.timeline__company {
  margin-top: 0.25rem;
  color: var(--success);
  font-weight: 600;
}

.timeline__period {
  font-size: 0.95rem;
  color: var(--text-muted);
}

.timeline__description {
  margin-top: 1rem;
  line-height: 1.75;
}

.timeline__list {
  margin-top: 1.15rem;
}

.timeline__list ul {
  list-style: none;
  display: grid;
  gap: 0.7rem;
}

.timeline__list li {
  display: flex;
  gap: 0.7rem;
  align-items: flex-start;
  color: var(--text-soft);
  line-height: 1.7;
}

.timeline__bullet {
  display: inline-block;
  width: 0.6rem;
  height: 0.6rem;
  border-radius: 999px;
  background: var(--success);
  margin-top: 0.45rem;
  flex-shrink: 0;
}

.timeline__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-top: 1.2rem;
}

.timeline__tags span {
  padding: 0.45rem 0.7rem;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(255, 255, 255, 0.05);
  color: var(--text-soft);
  font-size: 0.86rem;
}

@media (min-width: 768px) {
  .timeline__header {
    flex-direction: row;
    justify-content: space-between;
    align-items: flex-start;
  }
}
</style>
