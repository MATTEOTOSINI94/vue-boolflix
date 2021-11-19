<template>
  <div id="app">
    <Head @callMe="searchAll"></Head>
   
      <Card :moviees="this.movies" :serie="this.series" :flag="this.flags" :findValue="this.value" :cardBg="this.copertina" :funzioneTry="this.checkTitle" ></Card>
  
    
    <!-- <input type="text"  v-model="filterBar" @keyup.enter="searchAll"> -->
    <!-- <ul class="text-center row">
      <h1>FILM..</h1>
      <li class="col-3" v-for="(movie) in movies" :key="movie.id">
        <h2>titolo:{{movie.title}}</h2>
           <p>Titolo Originale: ({{movie.original_title}}) </p> 
           Bandiera:<img class="flag" :src="flags[movie.original_language] || flags.default" alt=""> {{movie.original_language}} <br>
           <span><i v-for="(voto) in value(movie.vote_average)" :key="voto.id"  class="fa fa-star" aria-hidden="true"></i><i v-for="voti in (5- value(movie.vote_average)) " :key="voti.id" class="fa fa-star-o" aria-hidden="true"></i> </span>
           voto: {{value(movie.vote_average)}}
           <img :src="copertina(movie.poster_path)" alt="">
      </li>
        <h1>SERIE TV..</h1>
       <li class="col-3" v-for="(series) in series" :key="series.id">
          {{series.name}} ({{ series.original_name}}) 
          <img class="flag" :src="flags[series.original_language] || flags.default" alt="">
          {{series.original_language}} <br>
           <span><i v-for="(voto) in value(series.vote_average)" :key="voto.id"  class="fa fa-star" aria-hidden="true"></i><i v-for="voti in (5- value(series.vote_average)) " :key="voti.id" class="fa fa-star-o" aria-hidden="true"></i> </span>
          {{value(series.vote_average)}}
          <img :src="copertina(series.backdrop_path)" alt=""> 
       </li>

    </ul> -->
  </div>
</template>

<script>

import axios from 'axios'
import Head from "./components/Head.vue"
import Card from "./components/card.vue"

// import { filter } from 'vue/types/umd'

export default {
  name: 'App',

  components:{
    Head,
    
    Card
  },
 data(){
   return{

     keyApi:"c1f56e9f69a038bc79759d802d8810c2",
     urlApi:"https://api.themoviedb.org/3",
     movies:[],
     series:[],
     flags:{
       en:require("./assets/en.png"),
       fr:require("./assets/fr.svg"),
       ja:require("./assets/jap.png"),
       es:require("./assets/sp.jpg"),
       default:require("./assets/default.png"),
     }
   }
  },

  methods:{

    value(numero){
      let filterNumber = numero / 2
      return  Math.round(filterNumber)
      
    },


    copertina(path){
      if (path === null) {
        return urlImg = "https://www.nato-pa.int/sites/default/files/default_images/default-image.jpg"
      }
      let url = "https://image.tmdb.org/t/p/w342/" ;
      let urlImg =  url + path
      return urlImg

    },
    checkTitle(movieTitle,title){ 
        if (movieTitle === title) {
          return title = ""
        }
        else{
          return title
        }
     },
    

    searchAll(filter){
      if (filter === "") {
          return this.movies  = [],
                  this.series = []
      }
        this.filmCall("/search/movie","movies",filter)
        this.filmCall("/search/tv","series",filter)
    },

    filmCall(tipologia,contenitore,filter){ axios.get(this.urlApi + tipologia,{
       params:{
         api_key: this.keyApi,
         query: filter,
         lenguage: "it"
       }
     }).then(lista => {
       this[contenitore] = lista.data.results
     })},
  },


 
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "~font-awesome/css/font-awesome.css";

#app {
  
 .flag{
   width: 50px;
 }
}
</style>
