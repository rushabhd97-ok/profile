<script setup lang="ts">
const props = defineProps<{
  title?: string
  subtitle?: string
  accent?: string
  large?: boolean
}>()
</script>

<template>
  <article :class="['glass-card', { large: props.large }]">
    <div v-if="props.accent" class="accent">{{ props.accent }}</div>
    <div class="content">
      <h3 v-if="props.title">{{ props.title }}</h3>
      <p v-if="props.subtitle">{{ props.subtitle }}</p>
      <div v-if="$slots.default" class="slot-content">
        <slot />
      </div>
    </div>
  </article>
</template>

<style scoped>
.glass-card {
  position: relative;
  overflow: hidden;
  padding: 1.8rem;
  border-radius: 1.25rem;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 20px 60px rgba(2, 6, 23, 0.28);
  backdrop-filter: blur(18px);
  transition: transform 180ms ease, border-color 180ms ease;
}

.glass-card:hover {
  transform: translateY(-2px);
  border-color: rgba(255, 255, 255, 0.18);
}

.glass-card.large {
  grid-column: span 2;
}

.accent {
  font-size: 1.8rem;
  margin-bottom: 1.25rem;
  color: #f8fafc;
}

.content h3 {
  margin: 0 0 0.7rem;
  font-size: 1.2rem;
  font-weight: 700;
  color: #f8fafc;
}

.content p {
  color: #8b9dbe;
  line-height: 1.7;
  margin: 0;
}

.slot-content {
  margin-top: 1rem;
}

@media (max-width: 600px) {
  .glass-card.large {
    grid-column: span 1;
  }
}
</style>
