<template>

<div class="box-main">
  <div class="container">
    <ul class="text-center row m-0">


      <div v-if="moviees.length > 0 "> <h1 class="Light">FILM..</h1></div>
      <Cardmovie v-for="movie ,i in moviees" :key="i" 
       :dati="movie"
       :screenBg="cardBg" 
       :titleFunc="funzioneTry"
       :flags="flag"
       :findNumber=" findValue"
       ></Cardmovie>


      <div v-if="serie.length > 0 "> <h1>SERIE TV..</h1></div>
       <CardSeries v-for="series in serie" :key="series.i"
       :dati="series"
       :screenBg="cardBg" 
       :titleFunc="funzioneTry"
       :flags="flag"
       :findNumber=" findValue"
       >
       </CardSeries>


      </ul>
      </div>
    </div>
</template>

<script>
import Cardmovie from "./cardMovie.vue"
import CardSeries from "./cardSeries.vue"
export default {
    name:"Main",
    props:{
    
    moviees:Array,
    findValue:Function,
    serie:Array,
    flag:Object,
    cardBg:Function,
    funzioneTry:Function,

    },

components:{
  Cardmovie,
  CardSeries
},





    

}


</script>

<style lang="scss">

.box-main{
  min-height: calc(100vh - 76px);
  background: grey;
}
.card-box{
    position: relative;
    list-style: none;
     cursor: pointer;
        width: 320px;
        height:480px;


        h2,p{
          color: white;
        }

}

.front{

  img{
    height: 100%;
    object-fit: cover;
    object-position: center;
    width: 100%;
  }
}

       

    .middle{
        position: absolute;
        left:50%;
        bottom: 50%;
        transform: translate(-50%, 50%);
    }

   .front, .back{
        width:100%;
        height: 100%;
        overflow:hidden;
        backface-visibility: hidden;
        position:absolute;
        transition: transform .5s linear;
        bottom: 0;
        left: 0;
        }
        
        .back{
        background:rgba(0, 0, 0, 0.748);
        transform:rotateY(180deg);
}

.card-box:hover > .front{
  transform: perspective(600px) rotateY(-180deg);
}
.card-box:hover > .back{
  transform: perspective(600px) rotateY(0deg);
}

.flag-full{
    color: yellow;
}
.stars-empty{
  color: white;
}
</style>

