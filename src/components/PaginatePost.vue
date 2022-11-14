<script setup>
const props = defineProps(['inicio', 'fin', 'maxPosts'])
const emit = defineEmits(['next', 'prev'])
</script>
<template >
  <div class="justify-content-end">
    <div class="btn-group" role="group" aria-label="Basic example">
      <button @click="emit('prev')" type="button" class="btn btn-outline-primary"
        :disabled="props.inicio === 0">Previus</button>
      <button @click="emit('next')" type="button" class="btn btn-outline-primary"
        :disabled="props.fin >= props.maxPosts">Next</button>
    </div>
  </div>
</template>
<style>

</style>