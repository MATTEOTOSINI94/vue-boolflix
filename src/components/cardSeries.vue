<template>
      
        <li class="col-4 card-box" @mouseover="getSeriesActor(dati.id)">
            <div class="front">
                  <img :src="screenBg(dati.backdrop_path)" alt=""> 
            </div>
            <div class="back middle">
              <div class="back-content middle">
                  <h2>{{dati.name}}</h2> 
                  <p>{{titleFunc(dati.name,dati.original_name)}}</p>
                  <p v-for="attori in actorSeries.slice(0,5)" :key="attori.i">{{attori.name}}</p>
                  <img class="flag" :src="flags[dati.original_language] || flags.default" alt=""> {{dati.original_language}} <br>
                  <span><i v-for="(voto) in findNumber(dati.vote_average)" :key="voto.id"  class="fa fa-star flag-full" aria-hidden="true"></i><i v-for="voti in (5- findNumber(dati.vote_average)) " :key="voti.id" class="fa fa-star-o stars-empty" aria-hidden="true"></i> </span>
                  {{findNumber(dati.vote_average)}}
              </div>
            </div>
          
        </li>
</template>

<script>
import axios from "axios"
export default {
    name: "CardSeries",


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
         actorSeries:[],
        }
    },


    methods:{

        getSeriesActor(id){
            axios.get(this.urlApi +"/tv/"+ id + "/credits",{
                params:{
                    api_key:this.keyApi
                }
            }).then((actors) => {
                this.actorSeries = actors.data.cast

                console.log(actors)
            })
        }

    }


    
}
</script>

<style lang="scss"  >
   
</style>

