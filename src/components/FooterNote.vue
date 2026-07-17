<script setup lang="ts">
import IconEmail from './icons/IconEmail.vue'
import IconGitHub from './icons/IconGitHub.vue'
import IconLinkedin from './icons/IconLinkedin.vue'

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
              <h4>Available for new opportunities</h4>
              <h3>Let’s build something polished and lasting.</h3>
              <p>
                I enjoy working on products where product thinking, polished UI, and reliable engineering all matter.
              </p>
            </div>

            <div class="footer__connect">
              <h4 class="sr-only">Connect</h4>
              <ul class="social-icons">
                <li>
                  <a href="https://linkedin.com/in/rushabh-dedhia-ab108314b/" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn" title="LinkedIn" class="icon-link">
                    <IconLinkedin :size="24" />
                  </a>
                </li>
                <li>
                  <a href="https://github.com/rushabhd97-ok" target="_blank" rel="noopener noreferrer" aria-label="GitHub" title="GitHub" class="icon-link">
                    <IconGitHub :size="24" />
                  </a>
                </li>
                <li>
                  <a href="mailto:rushabh.lucifer@gmail.com" aria-label="Email" title="Email" class="icon-link">
                    <IconEmail :size="24" />
                  </a>
                </li>
              </ul>
            </div>
      </div>

      <div class="footer__meta">
        <p>© 2026 Rushabh Dedhia. Crafted with care.</p>
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

.footer__intro h4 {
  margin: 0.3rem 0 0.8rem;
  font-size: 0.8rem;
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

/* New styles for centered intro and social icons */
.footer__intro {
  text-align: center;
}

.footer__connect {
  display: flex;
  align-items: center;
  justify-content: center;
}

.social-icons {
  list-style: none;
  display: flex;
  gap: 0.8rem;
  padding: 0;
  margin: 0;
}

.icon-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2.4rem;
  height: 2.4rem;
  color: var(--text-soft);
  border-radius: 0.5rem;
  transition: color 150ms ease, background 150ms ease;
}

.icon-link:hover {
  color: var(--text);
  background: rgba(255, 255, 255, 0.03);
}

.sr-only {
  position: absolute !important;
  width: 1px !important;
  height: 1px !important;
  padding: 0 !important;
  margin: -1px !important;
  overflow: hidden !important;
  clip: rect(0, 0, 0, 0) !important;
  white-space: nowrap !important;
  border: 0 !important;
}

.footer__meta a {
  color: var(--text-soft);
}

@media (min-width: 900px) {
  .footer__panel {
    grid-template-columns: 1fr auto;
    align-items: center;
  }

  .footer__meta {
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
}
</style>
