<script setup>
import { RouterLink } from 'vue-router'
import { useGetData } from '../composables/getData'

const { data, getData, loading, error } = useGetData()
getData('https://pokeapi.co/api/v2/pokemon')
</script>

<template>
  <h1>Pokemons</h1>
  <p v-if="loading">Cargando...</p>
  <div v-if="error" class="alert alert-danger mt-2">{{ error }}</div>
  <div v-if="data">
    <ul class="list-group">
      <li v-for="pokemon in data.results" key="pokemon.name" class="list-group-item">
        <RouterLink :to="`/pokemons/${pokemon.name}`">{{ pokemon.name }}</RouterLink>
      </li>
    </ul>
    <div class="py-4">
      <button
        :disabled="!data.previous"
        @click="getData(data.previous)"
        class="btn btn-outline-success me-2"
      >
        Prev
      </button>
      <button :disabled="!data.next" @click="getData(data.next)" class="btn btn-outline-success">
        Next
      </button>
    </div>
  </div>
</template>
