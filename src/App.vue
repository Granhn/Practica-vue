<script setup>
import { onMounted, ref } from 'vue';

import BlogPost from './components/BlogPost.vue';
import PaginatedPost from './components/PaginatedPost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue'

const posts = ref([])
const favorito = ref('')
const postXPage = ref(10);
const inicio = ref(0)
const fin = ref(10)
const loading = ref(true);

const cambiarFavorito = titulo =>{
  favorito.value = titulo;
}

const avanzarPagina = () =>{
  inicio.value = inicio.value + postXPage.value;
  fin.value = fin.value +postXPage.value;
}

const retrocederPagina = () =>{
  inicio.value = inicio.value - postXPage.value;
  fin.value = fin.value - postXPage.value;
}
onMounted(async() =>{
  loading.value = true;
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()

  } catch(error){
    console.log(error)
  } finally{
    setTimeout(() =>{
      loading.value = false
    },2000)
    
  }
  
    
  
})




</script>

<template>

  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h2>Mi post favorito : {{ favorito }}</h2><br>
    <PaginatedPost class="mb-2"
      @next="avanzarPagina"
      @prev="retrocederPagina"  
      :inicio="inicio"
      :fin="fin"
      :postsLength="posts.length"
    ></PaginatedPost>

    <br>

    <BlogPost
      v-for="post in posts.slice(inicio,fin)"
      :key="post.id"
      :title="post.title"
      :id = "post.id"
      :body = "post.body"
      @cambiarFavoritoNombre="cambiarFavorito" 
      :cambiarFavorito="cambiarFavorito"
      class="mb-2"
    >

    </BlogPost>  
  </div>
  
  
</template>