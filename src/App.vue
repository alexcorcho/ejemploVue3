<script setup>
import {ref} from 'vue';

import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue'

const posts = ref([]);
const postXpage = 10
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true)
const favorito = ref("");
const cambiarFavorito = (title) => {
  favorito.value = title;
};
const next = () =>{
  inicio.value = inicio.value + postXpage
  fin.value = fin.value + postXpage
}

const pref = () =>{
  inicio.value = inicio.value - postXpage
  fin.value = fin.value - postXpage
}

fetch('https://jsonplaceholder.typicode.com/posts')
.then(res => res.json())
.then((data) => posts.value = data)
.catch(e => console.log(e))
.finally(()=> {
  setTimeout(()=> {
    loading.value =false
  }, 1000);
  });
</script>

<template>
<LoadingSpinner v-if="loading"></LoadingSpinner>
<div class="container" v-else>
  <h1>App</h1>
  <h2>Mis Post Favoritos: {{ favorito }}</h2>

  <PaginatePost class="mb-2" 
  @next="next" 
  @pref="pref" 
  :inicio="inicio" 
  :fin="fin" 
  :maxLength="posts.length">
  </PaginatePost>


  <BlogPost
  v-for="post in posts.slice(inicio, fin)"
  :key="post.id"
  :title="post.title"
  :id="post.id"
  :body="post.body"
  :cambiarFavorito="cambiarFavorito"
  class="mb-2"
  ></BlogPost>
</div> 
</template>