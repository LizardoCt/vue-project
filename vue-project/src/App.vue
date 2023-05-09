<script setup>
import BlogPost from './components/BlogPost.vue'
import PaginationPost from './components/PaginationPost.vue'
import LoaderSpinner from './components/LoaderSpinner.vue'
// import BtnCounter from './components/BtnCounter.vue';
import { computed, onMounted, ref } from 'vue'

const posts = ref([
  // {title: 'Blog 1', body: 'holabb'},
  // {title: 'Blog 2', body: 'comostas'},
  // {title: 'Blog 3', },
])

const postPage = 10
const inicio = ref(0)
const fin = ref(postPage)
const loading = ref(true)

const favorito = ref('')
const cambiarFavorito = (title) => {
  favorito.value = title
}

const next = () => {
  inicio.value = inicio.value + postPage
  fin.value = fin.value + postPage
}

const prev = () => {
  inicio.value += -postPage
  fin.value += -postPage
}

// opcion 1 fecth
/*fetch('https://jsonplaceholder.typicode.com/posts')
    .then(res => res.json())
    .then((data) => {
      posts.value = data;
    })
    .catch((err) => console.log(err))
    .finally(() => (loading.value = false))*/

// opcion 2 fetch async await
const URL = 'https://jsonplaceholder.typicode.com/posts'
onMounted(() => {
  fetchData()
})

const fetchData = async () => {
  try {
    const res = await fetch(URL)
    posts.value = await res.json()
  } catch (err) {
    console.log(err)
  } finally {
    loading.value = false
  }
}
fetchData()

const maxLength = computed(() => posts.value.length)
</script>

<template>
  <div class="container">
    <h1 class="pt-5">Vue.js</h1>
    <h2 class="py-4">Mi Post Favorito: {{ favorito }}</h2>
    <!-- <BtnCounter /> -->
    <!-- <BlogPost title="Blog-2" body="holabb" colorText="textRed" /> -->

    <LoaderSpinner v-if="loading" />

    <PaginationPost
      @prev="prev"
      @next="next"
      :inicio="inicio"
      :fin="fin"
      :maxLength="maxLength"
    />

    <BlogPost
      v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :id="post.id"
      :title="post.title"
      :body="post.body"
      @cambiarFavorito="cambiarFavorito"
      class="mb-3"
    />

    <p class="my-4 text-center">By <span class="text-primary">nene</span></p>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@700&display=swap');
h1 {
  color: rgb(152, 219, 138);
  font-family: 'Montserrat', sans-serif;
}
h2 {
  font-family: 'Montserrat', sans-serif;
}
</style>
