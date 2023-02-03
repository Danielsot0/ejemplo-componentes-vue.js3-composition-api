<script setup>
import {computed, onMounted, ref} from "vue";

import ButtonCounter from './components/ButtonCounter.vue';
import PaginatePost from './components/PaginatePost.vue';
import BlogPost from './components/BlogPost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts = ref([]);
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);

const favorite = ref("");

const CambialFavorites = (title) => {
  favorite.value = title;

}

const next = () => {
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
}
const prev = () => {
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage;
}

// onMounted(async() => {
//   loading.value = true;
//   try{
//     const res = await fetch('https://jsonplaceholder.typicode.com/posts')
//     posts.value = await res.json();
//   }
//   catch(error){
//     console.log(error);

//   }finally{
//     setTimeout(() => {
//       loading.value = false;
//     }, 2000);
//   }
// });
// fetch ('https://jsonplaceholder.typicode.com/posts')
//     .then(res => res.json())
//     .then(data => {
//       posts.value = data
//     })
//     .catch((e) => console.log(e))
//     .finally(() => {
//       setTimeout(() => {
//         loading.value = false;
//       },2000);
//     });
  
      const fetchData = async () => {
        try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json();
  }
  catch(error){
    console.log(error);

  }finally{
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }

      };

      fetchData();

    const maxLength = computed(() => 
      posts.value.length
    );

</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mis post Favorito: {{ favorite }}</h2>

    <PaginatePost class="mb-2"
    @next="next"
    @prev="prev"
    :inicio="inicio"
    :fin="fin"
    :maxLength="maxLength"></PaginatePost>



    <BlogPost
    v-for="post in posts.slice(inicio, fin)" 
    :key="post.id" 
    :title="post.title" 
    :id="post.id" 
    :body="post.body"
    @CambialFavoritesNombre="CambialFavorites"
    class="mb-2"></BlogPost>
    </div>
</template>  
