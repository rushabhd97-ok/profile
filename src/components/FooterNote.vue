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
                    <svg viewBox="0 0 24 24" width="28" height="28" fill="currentColor" aria-hidden="true">
                      <path d="M4.98 3.5C4.98 4.88 3.88 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1 4.98 2.12 4.98 3.5zM0 8h5v16H0V8zm7.5 0H12v2.2h.1c.6-1.1 2-2.2 4.1-2.2 4.4 0 5.2 2.9 5.2 6.6V24H17v-7.2c0-1.7 0-3.9-2.4-3.9-2.4 0-2.7 1.8-2.7 3.8V24H7.5V8z" />
                    </svg>
                  </a>
                </li>
                <li>
                  <a href="https://github.com" target="_blank" rel="noopener noreferrer" aria-label="GitHub" title="GitHub" class="icon-link">
                    <svg viewBox="0 0 24 24" width="28" height="28" fill="currentColor" aria-hidden="true">
                      <path d="M12 0C5.37 0 0 5.37 0 12c0 5.3 3.44 9.8 8.21 11.39.6.11.82-.26.82-.58v-2.02c-3.34.73-4.04-1.61-4.04-1.61-.55-1.38-1.34-1.75-1.34-1.75-1.09-.75.08-.74.08-.74 1.2.09 1.83 1.24 1.83 1.24 1.07 1.83 2.8 1.3 3.48.99.11-.78.42-1.3.76-1.6-2.66-.3-5.46-1.33-5.46-5.93 0-1.31.47-2.38 1.24-3.22-.12-.3-.54-1.52.12-3.17 0 0 1-.32 3.3 1.23A11.5 11.5 0 0112 6.84c1.02.005 2.05.14 3.01.41 2.3-1.55 3.3-1.23 3.3-1.23.66 1.65.24 2.87.12 3.17.77.84 1.24 1.9 1.24 3.22 0 4.61-2.8 5.62-5.47 5.92.43.37.81 1.1.81 2.22v3.29c0 .32.22.7.83.58C20.56 21.8 24 17.3 24 12 24 5.37 18.63 0 12 0z" />
                    </svg>
                  </a>
                </li>
                <li>
                  <a href="mailto:rushabh.lucifer@gmail.com" aria-label="Email" title="Email" class="icon-link">
                    <svg viewBox="0 0 24 24" width="28" height="28" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                      <path d="M4 4h16v16H4z" fill="none" />
                      <path d="M22 6l-10 7L2 6" />
                    </svg>
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
