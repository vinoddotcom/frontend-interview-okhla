<!-- filepath: d:\front-end-interview\pages\index.vue -->
<template>
    <div>
      <SearchBar @search="fetchMovies" />
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 mt-10">
        <div 
          v-for="movie in movies" 
          :key="movie.imdbID" 
          class="bg-white rounded-lg shadow-md overflow-hidden transition-transform duration-300 hover:shadow-xl hover:scale-105 cursor-pointer" 
          @click="selectMovie(movie)"
        >
          <div class="h-64 overflow-hidden bg-gray-200">
            <img 
              class="w-full h-full object-cover" 
              :src="movie.Poster !== 'N/A' ? movie.Poster : 'https://via.placeholder.com/300x450?text=No+Poster+Available'"
              :alt="movie.Title"
            >
          </div>
          <div class="p-4">
            <h3 class="text-lg font-bold truncate">{{ movie.Title }}</h3>
            <p class="text-gray-600">{{ movie.Year }}</p>
            <p class="text-gray-500 text-sm mt-1">{{ movie.Type }}</p>
          </div>
        </div>
      </div>
      <div v-if="movies.length === 0" class="text-center mt-10 text-gray-600">
        Search for movies to see results
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
    Type?: string;
  }
  
  const movies = ref<Movie[]>([])
  const selectedMovie = ref<Movie | null>(null)
  
  const fetchMovies = async (searchTerm: string) => {
    try {
      const response = await fetch(`http://www.omdbapi.com/?apikey=c99c97e1&s=${searchTerm}`)
      const data = await response.json()
      
      if (data.Response === "True") {
        movies.value = data.Search || []
      } else {
        movies.value = []
        console.error('Error fetching movies:', data.Error)
      }
    } catch (error) {
      console.error('Error fetching movies:', error)
      movies.value = []
    }
  }
  
  const selectMovie = async (movie: Movie) => {
    try {
      // Get detailed movie information
      const response = await fetch(`http://www.omdbapi.com/?apikey=c99c97e1&i=${movie.imdbID}`)
      const detailedMovie = await response.json()
      selectedMovie.value = detailedMovie
    } catch (error) {
      console.error('Error fetching movie details:', error)
      selectedMovie.value = movie
    }
  }
  </script>