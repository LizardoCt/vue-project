<script setup>
import { storeToRefs } from 'pinia'
import { useFavoritesStore } from '../store/favorites'
import { RouterLink } from 'vue-router'

const useFavorites = useFavoritesStore()

const { favorites } = storeToRefs(useFavorites)
const { remove } = useFavorites
</script>

<template>
  <h1>Favoritos</h1>
  <p v-if="favorites.length === 0">Sin favoritos</p>
  <ul v-else class="list-group">
    <li v-for="pokemon in favorites" :key="pokemon.id" class="list-group-item">
      <div>
        {{ pokemon.name }}
      </div>
      <div>
        <router-link
          :to="`/pokemons/${pokemon.name}`"
          class="btn btn-sm btn-outline-secondary me-2"
          >Ver más</router-link
        >
        <button @click="remove(pokemon.id)" class="btn btn-sm btn-outline-danger">Eliminar</button>
      </div>
    </li>
  </ul>
</template>
