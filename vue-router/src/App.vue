<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <nav class="navbar bg-dark navbar-dark py-3">
    <div class="container">
      <router-link class="navbar-brand" to="">
        <img
          src="@/assets/logo.svg"
          alt=""
          width="30"
          height="24"
          class="d-inline-block align-text-top"
        />
        VueJS PokeApi
      </router-link>
      <div>
        <router-link 
          to="/"
          active-class="active"
          class="me-3 btn btn-outline-secondary"
          >Home</router-link
        >
        <router-link
          to="/pokemons"
          active-class="active"
          class="me-3 btn btn-outline-secondary"
          >Pokemons</router-link
        >
        <router-link
          to="/favorites"
          active-class="active"
          class="btn btn-outline-secondary"
          >❤</router-link
        >
      </div>
    </div>
  </nav>
  <div class="container text-center mt-4">
    <RouterView />
  </div>
</template>

<style scoped></style>
