<script setup>
import { ref } from 'vue'
const hover = ref(false)
</script>
<template>
  <button class="btn" @mouseenter="hover = true" @mouseleave="hover = false">
    <slot name="icon" :hover="hover" random="hello"></slot>
    <slot>Click Me</slot>
  </button>
  {{ hover }}
</template>
