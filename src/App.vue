<script setup>
import { ref } from 'vue'
import AppAlert from './components/AppAlert.vue'

const alerts = ref([
  {
    type: 'info',
    message: 'New software update available.'
  },
  {
    type: 'success',
    message: 'Your purchase has been confirmed!'
  },
  {
    type: 'warning',
    message: 'Warning: Invalid E-Mail address!'
  },
  {
    type: 'error',
    message: 'Error: Task failed successfully.'
  }
])

function handleClosed() {
  console.log('closed')
}
</script>

<template>
  <div class="p-5">
    <AppAlert
      v-for="alert in alerts"
      :key="alert.message"
      :type="alert.type"
      @closed="alerts = alerts.filter((a) => a.message !== alert.message)"
    >
      {{ alert.message }}
    </AppAlert>

    <pre>
      {{ alerts }}
    </pre>
  </div>
</template>

<style scoped></style>
