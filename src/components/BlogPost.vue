<script setup>

// defineProps(['title', 'body'])
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: 'Sin descripcion'
  }
})

const emit = defineEmits(['selectFav']);
</script>

<template >
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ id }} - {{ title }}</h5>
      <p>{{ body }}</p>
      <button @click="emit('selectFav', id)" class="btn btn-primary">Favorito</button>
    </div>
  </div>
</template>

<style >

</style>