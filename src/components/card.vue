<template>
<div class="container">
   <ul class="text-center row">
      <h1>FILM..</h1>
      <li class="col-3 card-box" v-for="(movie) in moviees " :key="movie.id">

          <div class="front">
              <img :src="cardBg(movie.poster_path)" alt="">
          </div>
        <div class="back middle">
          <div class="back-content middle">
                <h2>titolo:{{movie.title}}</h2>
                <p>({{movie.original_title}}) </p> 
                <img class="flag" :src="flag[movie.original_language] || flag.default" alt=""> {{movie.original_language}} <br>
                <span><i  v-for="(voto) in findValue(movie.vote_average)" :key="voto.id"  class="fa fa-star flag-full" aria-hidden="true"></i><i v-for="voti in (5- findValue(movie.vote_average)) " :key="voti.id" class="fa fa-star-o" aria-hidden="true"></i> </span>
                Rate: {{findValue(movie.vote_average)}}
          </div>    
        </div>
          
           
      </li>
        <h1>SERIE TV..</h1>
       <li class="col-3 card-box" v-for="(series) in serie" :key="series.id">
           <div class="front">
                <img :src="cardBg(series.backdrop_path)" alt=""> 
           </div>
           <div class="back middle">
             <div class="back-content middle">
                <h2>Titolo:{{series.name}}</h2> 
                <p> ({{ series.original_name}})</p>
                <img class="flag" :src="flag[series.original_language] || flag.default" alt=""> {{series.original_language}} <br>
                <span><i v-for="(voto) in findValue(series.vote_average)" :key="voto.id"  class="fa fa-star" aria-hidden="true"></i><i v-for="voti in (5- findValue(series.vote_average)) " :key="voti.id" class="fa fa-star-o" aria-hidden="true"></i> </span>
                Rate ;{{findValue(series.vote_average)}}
             </div>
           </div>
        
       </li>

    </ul>
    </div>
</template>

<script>
export default {
    name:"Card",
    props:{moviees:Array,
    findValue:Function,
    serie:Array,
    flag:Object,
    cardBg:Function}
}
</script>

<style lang="scss">
.card-box{
    position: relative;
    list-style: none;
     cursor: pointer;
        width: 342px;
        height:480px;
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
        background:#fff;
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

</style>

