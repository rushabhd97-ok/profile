<script setup lang="ts">
import ButtonLink from '@/components/ButtonLink.vue'

const highlights = ['Product-minded frontend engineering', 'Design systems and interactive UI', 'Performance-first delivery']
</script>

<template>
  <section id="hero" class="hero-section">
    <div class="hero-section__background" />
    <div class="container hero-section__content">
      <div class="hero-section__copy">
        <div class="hero-badge">
          <span class="hero-badge__dot" />
          Available for product-focused frontend work
        </div>

        <h1>Building calm, high-performing interfaces for modern products.</h1>

        <p>
          I’m Rushabh, a frontend engineer with 6+ years of experience crafting Vue, React, and Next.js experiences that feel sharp, intuitive, and easy to trust.
        </p>

        <div class="hero-actions">
          <ButtonLink href="mailto:rushabh.lucifer@gmail.com" variant="primary">Start a conversation</ButtonLink>
          <ButtonLink href="https://linkedin.com/in/rushabh-dedhia-ab108314b/" variant="secondary">View LinkedIn</ButtonLink>
        </div>

        <div class="hero-highlights">
          <div v-for="item in highlights" :key="item" class="pill">
            {{ item }}
          </div>
        </div>
      </div>

      <div class="hero-panel card">
        <div class="hero-panel__inner">
          <div class="hero-panel__header">
            <div>
              <p class="hero-panel__eyebrow">Current focus</p>
              <p class="hero-panel__title">Frontend systems & product delivery</p>
            </div>
            <span class="hero-panel__label">Available now</span>
          </div>

          <div class="hero-panel__stack">
            <div class="hero-panel__stack-header">
              <span>Core stack</span>
              <span>modern web</span>
            </div>
            <div class="hero-panel__tags">
              <span>Vue 3</span>
              <span>React</span>
              <span>Next.js</span>
              <span>TypeScript</span>
            </div>
          </div>
        </div>

        <div class="hero-panel__stats">
          <div>
            <p class="hero-panel__eyebrow">Delivery</p>
            <p class="hero-panel__value">6+ years</p>
            <p class="hero-panel__meta">Designing and shipping polished interfaces</p>
          </div>
          <div>
            <p class="hero-panel__eyebrow">Impact</p>
            <p class="hero-panel__value">50+ launches</p>
            <p class="hero-panel__meta">Across web platforms, dashboards, and commerce</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  position: relative;
  overflow: hidden;
  padding: 7.25rem 1.25rem 5.5rem;
}

.hero-section__background {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at top left, rgba(96, 165, 250, 0.2), transparent 36%),
    radial-gradient(circle at 85% 20%, rgba(217, 70, 239, 0.2), transparent 32%),
    linear-gradient(135deg, rgba(2, 6, 23, 0.98), rgba(11, 17, 32, 0.92));
}

.hero-section__content {
  position: relative;
  display: grid;
  gap: 2rem;
  align-items: center;
}

.hero-section__copy {
  max-width: 720px;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.65rem;
  border-radius: 999px;
  padding: 0.7rem 0.95rem;
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(255, 255, 255, 0.06);
  color: var(--text-soft);
  font-size: 0.95rem;
  box-shadow: 0 18px 48px rgba(2, 6, 23, 0.24);
}

.hero-badge__dot {
  width: 0.7rem;
  height: 0.7rem;
  border-radius: 999px;
  background: var(--success);
}

h1 {
  margin-top: 1.4rem;
  font-size: clamp(2.4rem, 4vw, 4rem);
  line-height: 1.02;
  letter-spacing: -0.04em;
  max-width: 740px;
}

.hero-section__copy p {
  margin-top: 1.2rem;
  font-size: 1.05rem;
  line-height: 1.8;
  max-width: 660px;
  color: var(--text-soft);
}

.hero-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.85rem;
  margin-top: 1.8rem;
}

.hero-highlights {
  display: flex;
  flex-wrap: wrap;
  gap: 0.7rem;
  margin-top: 1.6rem;
}

.hero-panel {
  padding: 1.25rem;
  background: rgba(5, 8, 22, 0.75);
}

.hero-panel__inner {
  padding: 1.2rem;
  border-radius: 1.2rem;
  background: linear-gradient(135deg, rgba(15, 23, 42, 0.95), rgba(30, 41, 59, 0.9));
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.hero-panel__header,
.hero-panel__stack-header {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
}

.hero-panel__eyebrow {
  margin: 0 0 0.25rem;
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.78rem;
  text-transform: uppercase;
  letter-spacing: 0.2em;
}

.hero-panel__title {
  margin: 0;
  color: var(--text);
  font-weight: 600;
}

.hero-panel__label {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.45rem 0.7rem;
  border-radius: 999px;
  border: 1px solid rgba(96, 165, 250, 0.24);
  background: rgba(96, 165, 250, 0.12);
  color: #bae6fd;
  font-size: 0.78rem;
  white-space: nowrap;
}

.hero-panel__stack {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(255, 255, 255, 0.05);
}

.hero-panel__stack-header {
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
}

.hero-panel__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
  margin-top: 0.85rem;
}

.hero-panel__tags span {
  padding: 0.45rem 0.7rem;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(255, 255, 255, 0.08);
  color: var(--text);
  font-size: 0.9rem;
}

.hero-panel__stats {
  display: grid;
  gap: 0.8rem;
  margin-top: 0.9rem;
}

.hero-panel__stats > div {
  padding: 1rem;
  border-radius: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(255, 255, 255, 0.04);
}

.hero-panel__value {
  margin: 0.35rem 0 0.3rem;
  font-size: 1.6rem;
  font-weight: 700;
  color: var(--text);
}

.hero-panel__meta {
  margin: 0;
  color: var(--text-soft);
  font-size: 0.95rem;
}

@media (min-width: 900px) {
  .hero-section__content {
    grid-template-columns: minmax(0, 1.1fr) minmax(320px, 0.9fr);
  }

  .hero-panel__stats {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
</style>
