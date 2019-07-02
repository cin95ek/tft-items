<template>
  <div id="app">
    <img alt="TFT" src="./assets/TFT.png">
    
    <transition name="fade">
    <Claim v-if="steep === 0"/>
    </transition>
    <transition name="fade">
    <Search @changed="onChange" v-if="steep != 1"/>
    </transition>
    <transition name="fade">
    <Checkboxes @changed="onChange" v-if="steep != 2"/>
    </transition>
  </div>
</template>

<script>
import Claim from '@/components/Claim.vue'
import Search from '@/components/Search.vue'
import Checkboxes from '@/components/Checkboxes.vue'
export default {
  name: 'app',
  components: {
    Claim,
    Search,
    Checkboxes,
  },

  data(){
    return{
      steep: 0 //when 1 use chekbox when 2 use input
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
