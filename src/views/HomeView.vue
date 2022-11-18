<template>
<div class="containertira">
            <div class="rowtira">
              <div class="containertira rounded">
                <div class="slidertira">
                  <div class="logostira w-30">
                    <router-link to="/movie/tt6443346">
                      <i class="fabtira"><img src="https://media.vandal.net/m/9-2022/2022991163975_1.jpg.webp"  width="210" height="210" alt="Black Adam"></i>
                    </router-link>
                    <router-link to="/movie/tt9271672">
                      <i class="fabtira"><img src="../prey-for-the-devil.jpg" width="210" height="210" alt="Prey For The Devil"></i>
                    </router-link>
                    <router-link to="/movie/tt13932410">
                      <i class="fabtira"><img src="https://m.media-amazon.com/images/M/MV5BNzE4MmMxYTgtMDQ3Ny00ODY4LTg3Y2QtNGYxYzEwYjE0ZWMyXkEyXkFqcGdeQXVyMTA0MjU0Ng@@._V1_.jpg" width="210" height="210" alt="El cuarto pasajero"></i>
                    </router-link>
                    <router-link to="/movie/tt10648342">
                      <i class="fabtira"><img src="https://wus-www.sway-cdn.com/s/Plo38ZCTsa8b7EKQ/images/kVOLFd_3A_bKJU?quality=1080&isThumbnail=True" width="210" height="210" alt="Thor"></i>
                    </router-link>
                    <router-link to="/movie/tt1745960">
                      <i class="fabtira"><img src="https://www.lahiguera.net/musicalia/artistas/varios/disco/12178/top_gun_maverick_music_from_the_motion_picture-portada.jpg" width="210" height="210" alt="top gun"></i>
                    </router-link>
                    <router-link to="/movie/tt9336032">
                      <i class="fabtira"><img src="https://www.ecartelera.com/carteles/17400/17456/001_m.jpg" width="210" height="210" alt="Asombrosa Elisa"></i>
                    </router-link>
                    <router-link to="/movie/tt13867056">
                      <i class="fabtira"><img src="https://es.web.img3.acsta.net/pictures/22/06/03/10/43/2149464.jpg" width="210" height="210" alt="No mires a los ojos"></i>
                    </router-link>
                    <router-link to="/movie/tt15128358">
                      <i class="fabtira"><img src="https://as01.epimg.net/meristation/imagenes/2022/09/30/reportajes/1664539297_898190_1664543339_noticia_normal.jpg" width="210" height="210" alt="modelo 77"></i>
                    </router-link>        
                    <router-link to="/movie/tt14104600">
                      <i class="fabtira"><img src="https://www.lavanguardia.com/peliculas-series/images/movie/poster/2022/10/w1280/4gQMa8BgSYe9CaDJRzJ9TvjS6LX.jpg" width="210" height="210" alt="una año una noche"></i>
                    </router-link>
                    <router-link to="/movie/tt11930126">
                      <i class="fabtira"><img src="https://decine21.com/img/upload/obras/alcarras-43867/alcarras-43867-c.jpg" width="210" height="210" alt="alcarras"></i>
                    </router-link>
                  </div>
               </div>
             </div>
           </div>
          </div> 

  <div class="home">
    <!-- <div class="feature-card">
      <router-link to="/movie/tt1477834"> 
        <img src="https://sm.ign.com/t/ign_es/movie/a/aquaman-1/aquaman-1_y9wr.300.jpg" alt="aquaman" 
         class="featured-img">
         <div class="detail">
          <h3>Aquaman</h3>
          <p>Arthur Curry, también conocido como Aquaman (Jason Momoa), es un habitante de un poderoso reino subacuático que recibe el nombre de la Atlántida. En esta película repleta de acción y aventura conoceremos sus orígenes, desde que era un niño criado por un hombre humano y considerado un paria por los suyos, hasta que crece y debe hacer frente a los problemas que han aparecido en su mundo.</p>
         </div>
      </router-link>
    </div> -->

<!-- @submit.prevent="SearchMovies()" -->
    <Form @submit="SearchMovies()" class="search-box">
       <Field type="text" name="search" placeholder="Buscar Película..." v-model="search" :rules="isRequired"/>
       <ErrorMessage class="form-required color-error" name="search" />
       <input type="submit" value="Search">
       
    </Form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <!-- {{ movie.Title }} -->
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster">
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>

import { ref } from "vue";
import env from '@/env.js';
import { Form, Field, ErrorMessage } from 'vee-validate';

export default {
  components: {
    Form,
    Field,
    ErrorMessage
  },
  methods: {
    /* onSubmit() {
      console.log('Submitting :(');
    }, */
    
    isRequired(value) {
      if (value && value.trim()) {
      return true;
      }else if(value<3 || value === ""){
      return 'El campo es requerido';
      }
    }
  },

setup (){

const search = ref("");
const movies = ref([]);

const SearchMovies = () =>{
  if(search.value != ""){
    //console.log(search.value);
    fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
    .then(response => response.json())
    .then(data =>{
      //console.log(data);
      movies.value = data.Search;
      /* search.value = ""; */
      console.log(movies.value);
      if(movies.value === undefined){
        alert("No hubo resultados en su búsqueda");
      }
       
    });
  }
 
}

return{
  search,
  movies,
  SearchMovies
}  



},

 
}
</script>

<script>

</script>

<style lang="scss">

 .home{
  .feature-card{
    position: relative;
    display: flex;
    justify-content: center;


    .featured-img{
     /*  display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0; */
     
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }

    .detail{
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      padding: 16px;
      background-color:  rgba(0,0,0,0.6);
      z-index: 1;

      h3{
        color: #fff;
        margin-bottom: 16px;
      }

      p{
        color: #fff;
      }
    }
  }

  .search-box{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input{
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"]{
        width: 40%;
        color: #fff;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;

        &::placeholder{
          color: #f3f3f3;
        }

        &:focus{
          box-shadow: 0px 3px 6px rgba(0,0,0,0.2);
        }
      }

      &[type="submit"]{
        width: 100%;
        max-width:150px;
        background-color: #42b883;
        padding: 16px;
        border-radius: 8px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;
        cursor: pointer;
        transition: .5s ease-in-out;

        &[type="submit"]:hover{
          background-color: #000;
        }

        &:active {
          background-color: #3B8070;
        }
      }
    }
  }

  .movies-list{
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;
  

    .movie{
      max-width: 20%; //estoy aquí
      flex: 1 1 50%;
      padding: 16px 8px;
    }

    .movie-link{
      display: flex;
      flex-direction: column; //row cambiar para mejorar en responsive
      height: 100%;
     

      .product-image{
        position: relative;
        display: block;
       
        img{
          display: block;
          width: 100%;
          height: 275px;
          object-fit: cover;
        }

        .type{
          position: absolute;
          padding: 8px 16px;
          background-color: #42B883;
          color: #fff;
          bottom: 16px;
          left: 0px;
          text-transform: capitalize;
        }
      }

      .detail{
        background-color: #496583;
        padding: 16px 8px;
        flex: 1 1 100%;
        border-radius: 0px 0px 8px 8px;

        .year{
          color: #aaa;
          font-size: 14px;
        }

        h3{
          color: #fff;
          font-weight: 600;
          font-size: 18px;
        }
      }
    }
  }

  .color-error{
    color: red;
  }
 }


 .containertira {
  overflow: hidden;
  background-color: #000;
  padding: 1rem;
  height: 40vh;
}
  .slidertira {
    animation: slidein 30s linear infinite;
    white-space: nowrap;
    width: 10%;
    
  }
    .logostira {
      width: 100%;
      display: inline-block;
      margin: 0px 0;
    }
      .fabtira {
        width: calc(100% / 5);
        margin: 1rem;
        animation: fade-in 0.5s cubic-bezier(0.455, 0.03, 0.515, 0.955) forwards;
        transition: border-color 0.15s ease-in-out, box-shadow 0.5s ease-in-out;
        cursor: pointer;
        border-radius: 1rem;
      }

      .fabtira:hover{
        box-shadow: 1px 2px 2px 0.55rem rgba(255, 255, 255, 0.5);
        border-radius: 1rem;
      }

      .w-30{
        width: 140%;
        height: 30%;
      }

@keyframes slidein {
  from {
    transform: translate3d(0, 0, 0);
  }
  to {
    transform: translate3d(-700%, 0, 0);
  }
}

@keyframes fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}


/*Responsivo*/

@media (min-width: 576px) {

}
@media (min-width: 768px) {

}
@media (min-width: 992px) {

}
@media (min-width: 1200px) {
}
@media (min-width: 1400px) {
 
}


</style>
