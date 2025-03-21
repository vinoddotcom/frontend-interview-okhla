<!-- filepath: d:\front-end-interview\components\MovieDetail.vue -->
<template>
  <TransitionRoot as="template" appear show="true">
    <Dialog as="div" class="fixed inset-0 z-10 overflow-y-auto" @close="close">
      <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
        <TransitionChild
          as="template"
          enter="ease-out duration-300"
          enterFrom="opacity-0"
          enterTo="opacity-100"
          leave="ease-in duration-200"
          leaveFrom="opacity-100"
          leaveTo="opacity-0"
        >
          <DialogOverlay class="fixed inset-0 bg-black bg-opacity-50 transition-opacity" />
        </TransitionChild>

        <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>

        <TransitionChild
          as="template"
          enter="ease-out duration-300"
          enterFrom="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
          enterTo="opacity-100 translate-y-0 sm:scale-100"
          leave="ease-in duration-200"
          leaveFrom="opacity-100 translate-y-0 sm:scale-100"
          leaveTo="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
        >
          <div class="inline-block align-bottom bg-white rounded-lg px-4 pt-5 pb-4 text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full sm:p-6">
            <div class="absolute top-2 right-2">
              <button @click="close" class="text-gray-500">X</button>
            </div>
            <img :src="movie.Poster" alt="Movie Poster" class="w-full h-auto" />
            <h2 class="text-2xl font-bold mt-4">{{ movie.Title }}</h2>
            <p><strong>Year:</strong> {{ movie.Year }}</p>
            <p><strong>Plot:</strong> {{ movie.Plot }}</p>
            <p><strong>Actors:</strong> {{ movie.Actors }}</p>
          </div>
        </TransitionChild>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'
import { Dialog, DialogOverlay, TransitionRoot, TransitionChild } from '@headlessui/vue'

interface Movie {
  imdbID: string;
  Poster: string;
  Title: string;
  Year: string;
  Plot?: string;
  Actors?: string;
}

defineProps<{ movie: Movie }>()
const emit = defineEmits(['close'])

const close = () => {
  emit('close')
}
</script>

<style scoped>
/* Add any additional styles if needed */
</style>