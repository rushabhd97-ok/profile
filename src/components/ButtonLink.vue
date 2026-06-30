<script setup lang="ts">
const props = defineProps<{
  href?: string
  label?: string
  variant?: 'primary' | 'secondary'
}>()
</script>

<template>
  <a v-if="props.href" :href="props.href" :class="['button', `button-${props.variant || 'secondary'}`]">
    <slot>{{ props.label }}</slot>
  </a>
  <button v-else :class="['button', `button-${props.variant || 'secondary'}`]">
    <slot>{{ props.label }}</slot>
  </button>
</template>

<style scoped>
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 999px;
  padding: 0.85rem 1.35rem;
  font-size: 0.95rem;
  font-weight: 600;
  transition: transform 180ms ease, background-color 180ms ease, border-color 180ms ease;
  text-decoration: none;
  cursor: pointer;
}

.button:hover {
  transform: translateY(-1px);
}

.button-primary {
  background: linear-gradient(135deg, #ffffff 0%, #dce7ff 100%);
  color: #050816;
  border: 1px solid rgba(255, 255, 255, 0.9);
}

.button-secondary {
  background: rgba(255, 255, 255, 0.06);
  color: #f8fafc;
  border: 1px solid rgba(255, 255, 255, 0.12);
}
</style>
