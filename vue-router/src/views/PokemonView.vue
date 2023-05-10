<script setup>
import { useRoute, useRouter } from 'vue-router'
import { useGetData } from '../composables/getData'
import { useFavoritesStore } from '../store/favorites'

const route = useRoute()
const router = useRouter()
const useFavorites = useFavoritesStore()

const { add, findPokemon } = useFavorites

const { data, loading, getData, error } = useGetData()

const back = () => {
  router.push('/pokemons')
}

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
</script>

<template>
  <p v-if="loading">Cargando...</p>
  <div v-if="error" class="alert alert-danger mt-2">No existe el pokemon</div>
  <div v-if="data">
    <img :src="data.sprites?.front_default" alt="" />
    <h1>Pokemon name: {{ $route.params.name }}</h1>
    <button
      :disabled="findPokemon(data.name)"
      @click="add(data)"
      class="btn btn-outline-danger mb-2"
    >
      ❤
    </button>
  </div>

  <button @click="back" class="btn btn-outline-secondary">Return</button>
</template>
