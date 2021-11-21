<template>
   
        
        <li class="col-4 card-box" @mouseover="getCredit(dati.id)" >
            <div class="front">
                <img :src="screenBg(dati.poster_path)" alt="">
            </div>
          <div class="back middle">
            <div class="back-content middle">
                  <h2>{{dati.title || dati.original_title}}</h2>
                  <div class="" v-if="castFilm.length > 0">  
                     <h5 >Attori:</h5>
                     <p class="m-0" v-for="attori,i in castFilm.slice(0,5)" :key="i">{{attori.name}}</p>
                  </div>
                  <p>{{titleFunc(dati.title,dati.original_title)}} </p> 
                  <img class="flag" :src="flags[dati.original_language] || flags.default" alt=""> {{dati.original_language}} <br>
                  <span><i  v-for="(voto) in findNumber(dati.vote_average)" :key="voto.id"  class="fa fa-star flag-full" aria-hidden="true"></i><i v-for="voti in (5- findNumber(dati.vote_average)) " :key="voti.id" class="fa fa-star-o stars-empty" aria-hidden="true"></i> </span>
                  {{findNumber(dati.vote_average)}}
            </div>    
          </div>
            
            
        </li>
    
</template>

<script>

import axios from 'axios'
export default {
    name: "Cardmovie",

    props:{
        screenBg: Function,
        titleFunc: Function,
        flags:Object,
        findNumber:Function,
        dati:Object

    },

    data(){
      return{
         keyApi:"c1f56e9f69a038bc79759d802d8810c2",
         urlApi:"https://api.themoviedb.org/3",
         castFilm:[],
         
         
      }
    },

    methods:{
  getCredit(id){
    axios.get(this.urlApi + "/movie/" + id +"/credits",{
       params:{
         api_key: this.keyApi,
       }
    }
    ).then((actors) =>{
      this.castFilm = actors.data.cast
      console.log( this.castFilm)
    })
  },


  

  


}
}
</script>

<style>

</style>