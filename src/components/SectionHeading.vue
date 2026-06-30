<script setup lang="ts">
const props = defineProps<{
  eyebrow?: string
  title: string
  description?: string
}>()
</script>

<template>
  <div class="section-heading">
    <p v-if="props.eyebrow" class="eyebrow">{{ props.eyebrow }}</p>
    <h2>{{ props.title }}</h2>
    <p v-if="props.description" class="description">{{ props.description }}</p>
  </div>
</template>

<style scoped>
.section-heading {
  max-width: 720px;
  margin-bottom: 2.5rem;
}

.eyebrow {
  margin-bottom: 0.75rem;
  color: #8b9dbe;
  text-transform: uppercase;
  letter-spacing: 0.24em;
  font-size: 0.8rem;
  font-weight: 600;
}

h2 {
  font-size: clamp(1.8rem, 2.4vw, 2.4rem);
  font-weight: 700;
  margin: 0 0 0.9rem;
  color: #f8fafc;
  letter-spacing: -0.03em;
}

.description {
  color: #8b9dbe;
  font-size: 1rem;
  line-height: 1.7;
}
</style>
