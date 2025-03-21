<!-- filepath: d:\front-end-interview\components\SearchBar.vue -->
<template>
    <div class="flex justify-center mt-10">
      <input
        v-model="searchTerm"
        placeholder="Search for a movie..."
        type="text"
        class="p-2 border border-gray-300 rounded"
        @keyup.enter="searchMovies"
      >
      <button
      class="ml-2 p-2 bg-blue-500 text-white rounded"
      @click="searchMovies"
      >Search</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref, defineEmits } from 'vue'
  
  const searchTerm = ref<string>('')
  
  const emit = defineEmits(['search'])
  
  const searchMovies = () => {
    emit('search', searchTerm.value)
  }
  </script>