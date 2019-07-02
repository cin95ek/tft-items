<template>
  <div class="hello">
    
    <h1>Just type item name or simply pick from list.</h1>
    <p>If you choose one method, the second one will disappear</p>
  </div>
</template>

<script>
export default {
  name: 'Claim',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.hello{
  padding-left: 5vw;
  padding-right: 5vw;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

img{
  max-width: 50%;
  height: auto;
}
</style>
