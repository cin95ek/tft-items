<template>
  <div id="app">
    <img alt="TFT" src="./assets/TFT.png">
    <Claim/>
    <Search/>
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
</style>
