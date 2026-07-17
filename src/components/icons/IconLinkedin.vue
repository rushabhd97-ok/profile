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
    fill="currentColor"
    aria-hidden="true"
  >
    <path d="M4.98 3.5C4.98 4.88 3.88 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1 4.98 2.12 4.98 3.5zM0 8h5v16H0V8zm7.5 0H12v2.2h.1c.6-1.1 2-2.2 4.1-2.2 4.4 0 5.2 2.9 5.2 6.6V24H17v-7.2c0-1.7 0-3.9-2.4-3.9-2.4 0-2.7 1.8-2.7 3.8V24H7.5V8z" />
  </svg>
</template>
