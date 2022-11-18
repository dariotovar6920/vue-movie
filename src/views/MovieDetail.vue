<template>
    <div class="movie-detail">
        <!-- Detail {{ $route.params.id }} -->
        <h2>{{ movie.Title }}</h2>
        <p><span>Año:</span> {{ movie.Year }}</p>
        <p><span>Categoría:</span> {{ movie.Genre }}</p>
        <p><span>Actores:</span> {{ movie.Actors }}</p>
        <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
        <p><span>Resumen:</span> {{ movie.Plot }}</p>
    </div>
    <div>
        <router-link to="/">
        <input type="button" value="Home">
        </router-link>
    </div>
    
</template>

<script>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router';
import env from '@/env.js';

    export default{
        setup (){
            const movie = ref({});
            const route = useRoute();

            onBeforeMount(() =>{
                 //console.log("before Mount");
                 fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
                 .then(response => response.json())
                 .then(data =>{
                    //console.log(data);
                    movie.value = data;
                 })
            });

            return {
                movie
            }
        }
    }
</script>

<style lang="scss">

.movie-detail {
    padding: 16px;

    h2{
        color: #fff;
        font-size: 28px;
        font-weight: 600;
        margin-bottom: 16px;
    }

    .featured-img{
        display: block;
        max-width: 200px;
        margin-bottom: 16px;
    }

    span{
        font-weight: bold;
        color: #fff;
    }

    p{
        color: #d1d1d1;
        font-size: 18px;
        line-height: 1.4;
    }

    input{
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      background-color: red;
    }
}

input{
    display: block;
    appearance: none;
    border: none;
    outline: none;
    background: none;

    &[type="button"]{
        width: 30%;
        max-width: 300px;
        background-color: #42b883;
        padding: 16px;
        border-radius: 8px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;
        cursor: pointer;

        &:active {
          background-color: #3B8070;
        }
      }
}

</style>