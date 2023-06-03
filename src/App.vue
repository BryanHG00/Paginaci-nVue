<script setup>
import { computed, onMounted, ref } from 'vue';

import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([])
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);
const fav = ref("");
const loading = ref(false);

const favorito = (title) =>{
  fav.value = title;
}

onMounted(async ()=>{
  loading.value = true;
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch(error){
    console.log(error);
  } finally{
    loading.value = false
  }
})

const next = () =>{
  inicio.value += postXpage;
  fin.value += postXpage;
}

const prev = () =>{
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage;
}

const postLen = computed(()=> posts.value.length);

</script>
<template>
  <LoadingSpinner v-if="loading" />
  <div v-else class="container">
    <h1>Mis posts:</h1>
    <h2>Post favorito: {{ fav }}</h2>
  <!-- dos puntos cuando hay que pasar un dato primitivo de javascrit (numero, bool, double) -->
  <!-- <BlogPost title="Post 01" :id="1" body="Descripcion 1" @fav="favorito" />
  <BlogPost title="Post 02" :id="2" body="Descripcion 2" @fav="favorito" />
  <BlogPost title="Post 03" :id="3" body="Descripcion 3" @fav="favorito" />
   para probar si funciona la parte de por defecto -->
  <!--<BlogPost title="Post 04" :id="4" @fav="favorito"/> -->
  <!-- <h2>Ciclando con for</h2> -->
  <PaginatePost @next="next" @prev="prev" :inicio="inicio" :fin="fin" :postlen="postLen"/>
  <BlogPost v-for="post in posts.slice(inicio,fin)"
  :key="post.id"
  :title="post.title"
  :id="post.id"
  :body="post.body"
  @fav="favorito"
  >
  </BlogPost>
  </div>
</template>
