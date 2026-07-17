<script setup lang="ts">
import IconEmail from './icons/IconEmail.vue'
import IconGitHub from './icons/IconGitHub.vue'
import IconLinkedin from './icons/IconLinkedin.vue'
import IconPhone from './icons/IconPhone.vue'

defineProps<{
  modelValue: boolean
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: boolean): void
}>()

const close = () => {
  emit('update:modelValue', false)
}
</script>

<template>
  <div v-if="modelValue" class="modal-backdrop" @click.self="close">
    <div class="modal-card" role="dialog" aria-modal="true" aria-labelledby="contact-title">
      <button class="modal-close" type="button" @click="close" aria-label="Close contact details">
        ×
      </button>

      <p class="modal-kicker">Frontend Developer</p>
      <h2 id="contact-title">Rushabh Jatin Dedhia</h2>

      <div class="modal-details">
        <a href="tel:+918652821301">
          <span class="detail-icon"><IconPhone :size="16" /></span>
          <span>Mobile: +91 8652821301</span>
        </a>
        <a href="mailto:rushabh.lucifer@gmail.com">
          <span class="detail-icon"><IconEmail :size="16" /></span>
          <span>Email: rushabh.lucifer@gmail.com</span>
        </a>
      </div>

      <div class="social-links" aria-label="Social links">
        <a href="https://www.linkedin.com" target="_blank" rel="noopener noreferrer" aria-label="Visit LinkedIn profile">
          <IconLinkedin :size="18" />
        </a>

        <a href="https://github.com" target="_blank" rel="noopener noreferrer" aria-label="Visit GitHub profile">
          <IconGitHub :size="18" />
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 100;
  display: grid;
  place-items: center;
  padding: 1rem;
  background: rgba(2, 6, 23, 0.78);
  backdrop-filter: blur(8px);
}

.modal-card {
  position: relative;
  width: min(100%, 28rem);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 1.25rem;
  padding: 1.6rem;
  background: rgba(9, 14, 29, 0.97);
  box-shadow: 0 24px 60px rgba(0, 0, 0, 0.35);
}

.modal-close {
  position: absolute;
  top: 0.8rem;
  right: 0.8rem;
  border: 0;
  border-radius: 999px;
  width: 2.1rem;
  height: 2.1rem;
  background: rgba(255, 255, 255, 0.08);
  color: var(--text);
  font-size: 1.2rem;
  cursor: pointer;
}

.modal-kicker {
  margin: 0 0 0.35rem;
  color: var(--accent);
  font-size: 0.82rem;
  font-weight: 700;
  letter-spacing: 0.16em;
  text-transform: uppercase;
}

.modal-card h2 {
  margin: 0 0 1rem;
  color: var(--text);
  font-size: 1.4rem;
}

.modal-details {
  display: grid;
  gap: 0.7rem;
  margin-bottom: 1.2rem;
}

.modal-details a {
  display: flex;
  align-items: center;
  gap: 0.65rem;
  color: var(--text-soft);
  text-decoration: none;
}

.modal-details a:hover {
  color: var(--text);
}

.detail-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  color: var(--accent);
}

.social-links {
  display: flex;
  gap: 0.8rem;
}

.social-links a {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2.6rem;
  height: 2.6rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.08);
  color: var(--text);
}

.social-links svg {
  width: 1.1rem;
  height: 1.1rem;
}
</style>
