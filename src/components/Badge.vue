<template>
  <span :class="[
    'rounded-full text-white inline-flex px-3 py-1', {
      'bg-green-600': status.toLowerCase() === 'success',
      'bg-red-600': status.toLowerCase() === 'failure'
    },
  ]">{{ message }}</span>
</template>

<script setup>
defineProps({
  status: {
    type: String,
    required: true
  },
  message: {
    type: String,
    required: true
  },
})
</script>
