<script setup lang="ts">
defineProps<{
  title?: string
  description?: string
}>()
</script>

<template>
  <footer class="footer">
    <div class="container footer__inner">
      <div class="footer__panel card">
        <div class="footer__intro">
          <p class="footer__eyebrow">Available for new opportunities</p>
          <h3>Let’s build something polished and lasting.</h3>
          <p>
            I enjoy working on products where product thinking, polished UI, and reliable engineering all matter.
          </p>
        </div>

        <div>
          <h4>Connect</h4>
          <ul>
            <li><a href="https://linkedin.com/in/rushabh-dedhia-ab108314b/" target="_blank" rel="noopener noreferrer">LinkedIn</a></li>
            <li><a href="https://github.com" target="_blank" rel="noopener noreferrer">GitHub</a></li>
            <li><a href="mailto:rushabh.lucifer@gmail.com">Email</a></li>
          </ul>
        </div>

        <div>
          <h4>Experience</h4>
          <ul>
            <li>PRPM - OneKirana</li>
            <li>Swegon Bluebox</li>
            <li>CodeArray Technologies</li>
          </ul>
        </div>

        <div>
          <h4>Stack</h4>
          <ul>
            <li>React / Next.js</li>
            <li>Vue / Nuxt</li>
            <li>TypeScript / CSS</li>
          </ul>
        </div>
      </div>

      <div class="footer__meta">
        <p>© 2026 Rushabh Dedhia. Crafted with care.</p>
        <a href="/resume.pdf">Download resume</a>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  padding: 1.25rem 1.25rem 2rem;
}

.footer__inner {
  display: grid;
  gap: 1.25rem;
}

.footer__panel {
  display: grid;
  gap: 1.5rem;
  padding: 1.4rem;
  background: rgba(5, 8, 22, 0.82);
}

.footer__intro h3 {
  margin: 0.3rem 0 0.8rem;
  font-size: 1.5rem;
}

.footer__intro p {
  margin: 0;
  max-width: 34rem;
  line-height: 1.75;
}

.footer__eyebrow {
  margin: 0;
  color: rgba(255, 255, 255, 0.75);
  font-size: 0.8rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
}

.footer__panel h4 {
  margin: 0 0 0.7rem;
  font-size: 0.9rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.75);
}

.footer__panel ul {
  list-style: none;
  display: grid;
  gap: 0.6rem;
}

.footer__panel li,
.footer__panel a {
  color: var(--text-soft);
}

.footer__panel a:hover {
  color: var(--text);
}

.footer__meta {
  display: flex;
  flex-direction: column;
  gap: 0.45rem;
  padding-top: 0.7rem;
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.95rem;
}

.footer__meta a {
  color: var(--text-soft);
}

@media (min-width: 900px) {
  .footer__panel {
    grid-template-columns: 1.2fr 0.8fr 0.8fr 0.8fr;
  }

  .footer__meta {
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
}
</style>
