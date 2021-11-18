<template>
  <header>
      <div class="block-head">
        <div class="container">
            <h1>BoolFlix</h1>
                <div class="ms-auto">
                    <input placeholder="Inizia la tua ricerca.." type="text" v-model="filterBar" @keyup.enter="$emit('callMe', filterBar)">
                </div>
        </div>
      </div>
  </header>
</template>

<script>
export default {
    name:"Head",

        data(){
            return {
                filterBar:""
            }
        }

    

    
}
</script>

<style lang="scss" scoped>
    .block-head{
        background: black;
        padding: 10px;
        
        .container{

            display: flex;
            align-items: center;

              h1{
            color: red;
        }
        }

        
        
    }

      
    
</style>

