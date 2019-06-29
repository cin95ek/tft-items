<template>
  <div id="app">
    <img alt="TFT" src="./assets/TFT.png">
    
    <transition name="fade">
    <Claim v-if="steep === 0"/>
    </transition>
    
    <Search @changed="onChange"/>
  </div>
</template>

<script>
import Claim from '@/components/Claim.vue'
import Search from '@/components/Search.vue'
export default {
  name: 'app',
  components: {
    Claim,
    Search,
  },

  data(){
    return{
      steep: 0
    }
  },


   methods: {
    onChange (value) {
      
      this.steep = value;
     
    }
  }
}


</script>

<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  justify-content: center;
}



img{
  max-width: 50%;
  
}

@media (min-width: 768px){
  img{
    max-width: 30%;
  }
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .3s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
