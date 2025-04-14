<script setup lang="ts">
  const emit = defineEmits(['clicked']);
</script>

<template>
  <button class="bg-amber-400 text-amber-900 font-bold font-mono py-2 px-4 border-2 shadow-[3px_3px_0_0] hover:shadow-[2px_2px_0_0] active:shadow-none shadow-amber-900 hover:shadow-amber-900 border-amber-900 rounded"
          @click="emit('clicked')"
  >
    <slot/>
  </button>
</template>

