<script setup>
import { ref, computed } from 'vue'
import AppIconError from './Icons/AppIconError.vue'
import AppIconSuccess from './Icons/AppIconSuccess.vue'
import AppIconWarning from './Icons/AppIconWarning.vue'
import AppIconInfo from './Icons/AppIconInfo.vue'

const props = defineProps({
  type: { type: String, default: 'info' }
})

const alertType = computed(() => {
  return {
    info: 'alert-info',
    warning: 'alert-warning',
    success: 'alert-success',
    error: 'alert-error'
  }[props.type]
})

const alertIcon = computed(() => {
  return {
    info: AppIconInfo,
    warning: AppIconWarning,
    success: AppIconSuccess,
    error: AppIconError
  }[props.type]
})

const emit = defineEmits(['closed'])

const closed = ref(false)

function hideAlert() {
  closed.value = true
  emit('closed')
}
</script>

<template>
  <div v-if="!closed" role="alert" :class="`mb-5 alert ${alertType}`">
    <component :is="alertIcon"></component>
    <span><slot></slot></span>
    <button @click="hideAlert">ⅹ</button>
  </div>
</template>
