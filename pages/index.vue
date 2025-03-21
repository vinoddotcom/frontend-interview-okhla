<!-- filepath: d:\front-end-interview\pages\index.vue -->
<template>
    <div>
      <SearchBar @search="fetchMovies" />
      <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-4 mt-10">
        <div v-for="movie in movies" :key="movie.imdbID" @click="selectMovie(movie)" class="cursor-pointer">
          <img 
          class="w-full h-auto" 
          :src="movie.Poster"
          alt="Movie Poster"
            >
          <h3 class="text-lg font-bold">{{ movie.Title }}</h3>
          <p>{{ movie.Year }}</p>
        </div>
      </div>
      <MovieDetail v-if="selectedMovie" :movie="selectedMovie" @close="selectedMovie = null" />
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue'
  import SearchBar from '@/components/SearchBar.vue'
  import MovieDetail from '@/components/MovieDetail.vue'
  
  interface Movie {
    imdbID: string;
    Poster: string;
    Title: string;
    Year: string;
    Plot?: string;
    Actors?: string;
  }
  
  const movies = ref<Movie[]>([])
  const selectedMovie = ref<Movie | null>(null)
    // const YOUR_API_KEY =  useRuntimeConfig().apiSecret
  const fetchMovies = async (searchTerm: string) => {
    const response = await fetch(`http://www.omdbapi.com/?apikey=c99c97e1&s=${searchTerm}`)
    const data = await response.json()
    movies.value = data.Search
  }
  
  const selectMovie = (movie: Movie) => {
    selectedMovie.value = movie
  }
  </script>