<script setup lang="ts">
withDefaults(defineProps<{ size?: string | number }>(), {
  size: 24,
})
</script>

<template>
  <svg
    :width="size"
    :height="size"
    viewBox="0 0 24 24"
    fill="none"
    stroke="currentColor"
    stroke-width="1.8"
    stroke-linecap="round"
    stroke-linejoin="round"
    aria-hidden="true"
  >
    <path d="M22 16.92v2.84a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6A19.79 19.79 0 0 1 2.25 4.18 2 2 0 0 1 4.2 2h2.84a2 2 0 0 1 2 1.72c.12 1.08.37 2.13.74 3.14a2 2 0 0 1-.45 2.08L7.2 9.12a16 16 0 0 0 6 6l.18-.18a2 2 0 0 1 2.08-.45c1 .37 2.06.62 3.14.74A2 2 0 0 1 22 16.92Z" />
  </svg>
</template>
