<template>
  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
    :class="props.class">
    <path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12.75l6 6 9-13.5" />
  </svg>
</template>

<script setup lang="ts">
const props = defineProps({
  class: { type: String, required: false, default: "w-6 h-6" },
})
</script>

<style scoped></style>