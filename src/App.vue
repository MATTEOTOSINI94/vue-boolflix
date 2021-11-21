<template>
  <div id="app">
    <Head @callMe="searchAll"></Head>
      <Main :moviees="this.movies" :serie="this.series" :flag="this.flags" :findValue="this.value" :cardBg="this.copertina" :funzioneTry="this.checkTitle" ></Main>
  </div>
</template>

<script>

import axios from 'axios'
import Head from "./components/Head.vue"
import Main from "./components/Main.vue"


export default {
  name: 'App',

  components:{
    Head,
  
    Main
  },
 data(){
   return{

     keyApi:"c1f56e9f69a038bc79759d802d8810c2",
     urlApi:"https://api.themoviedb.org/3",
     movies:[],
     series:[],
     Actors:[],
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
         lenguage: "it",
         
         
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
