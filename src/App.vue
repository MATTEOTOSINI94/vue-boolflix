<template>
  <div id="app">

    <input type="text"  v-model="filterBar" @keyup.enter="searchAll">
    <ul>
      <h1>FILM..</h1>
      <li v-for="(movie) in movies" :key="movie.id">
        {{movie.title}} ({{movie.original_title}}) <img :src="flags[movie.original_language] || flags.default" alt=""> {{movie.original_language}} <br>
        {{movie.vote_average}}
      </li>
        <h1>SERIE TV..</h1>
      <li v-for="(series) in series" :key="series.id">
      {{series.name}} ({{ series.original_name}}) 
      <img :src="flags[series.original_language] || flags.default" alt="">
      {{series.original_language}} <br>
      {{series.vote_average}}
      </li>

    </ul>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'App',
 data(){
   return{
     keyApi:"c1f56e9f69a038bc79759d802d8810c2",
     urlApi:"https://api.themoviedb.org/3",
     filterBar:"",
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

    searchAll(){
      if (this.filterBar === "") {
          return this.movies  = [],
                  this.series = []
      }
        this.filmCall("/search/movie","movies")
        this.filmCall("/search/tv","series")
    },

    filmCall(tipologia ,contenitore){ axios.get(this.urlApi + tipologia,{
       params:{
         api_key: this.keyApi,
         query: this.filterBar
       }
     }).then(lista => {
       this[contenitore] = lista.data.results
     })},
  },


   mounted(){
   
 }
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
#app {
  h1{color: black;}
  img{
    width: 100px;
  }
}
</style>
