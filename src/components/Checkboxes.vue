<template>
    <div>
      <ul>
        <li v-for="item in baseItems" :key="item.name">
            <input type="radio" :name="item.name" :id="item.name" :value="item.name" v-model="picked" @change="handleClick" >
            <label :for="item.name" ><img :src="item.image" alt=" "></label>
            <div></div>
        </li>
        </ul>

        <div class="container">
          <div class="item" v-for="item in results" :key="item.name">
          
          
          <p class="itemName">{{item.name}}</p>
          <div class="wynik">
          
          <span id="symbol">+</span>
          <img :src="item.item1Img" :alt="item.item1" v-if="item.item1.toUpperCase().includes(picked.toUpperCase()) && item.item2.toUpperCase().includes(picked.toUpperCase())">
          <img :src="item.item1Img" :alt="item.item1" :title="item.item2" v-else-if="!item.item1.toUpperCase().includes(picked.toUpperCase())">
          <img :src="item.item2Img" :alt="item.item2" :title="item.item2" v-else-if="!item.item2.toUpperCase().includes(picked.toUpperCase())">
          <span id="symbol">=</span>
          <img :src="item.image" :alt="item.name" :title="item.name">
          <div class="desc">
            
            <p class="itemDesc">{{item.description}}</p>
  
          
          
          </div>
            </div> 

          </div> 
        </div>
        
    </div>
</template>

<script>
import items from '../assets/items.json'
import baseItems from '../assets/baseItems.json'
export default {
    name: 'Checkboxes',

data(){
    return{
      picked: '',
      results:[],
      items: items,
      baseItems: baseItems,

    }
},  


methods:{
handleClick: function(event) {
  this.$emit('changed', '1') 
  let chose = this.picked.toUpperCase();
  this.results.length = 0;
  console.log(chose)
  for (let index = 0; index < items.length; index++) {
    let temp1 = this.items[index].item1.toUpperCase();
    let temp2 = this.items[index].item2.toUpperCase();
    if (chose.includes(temp1) && chose.includes(temp2) ) {
      this.results.push(this.items[index]);
    }else if (chose.includes(temp1) || chose.includes(temp2) ) {
      this.results.push(this.items[index]);
     
    }
    
  }
console.log(this.results)
}
},
mounted: function () {
  for (let index = 0; index < this.items.length; index++) {
    for (let index2 = 0; index2 < this.baseItems.length; index2++) {
     if (this.items[index].item1 == this.baseItems[index2].name) {
       this.items[index].item1Desc = this.baseItems[index2].description
       this.items[index].item1Img = this.baseItems[index2].image
     }
     if (this.items[index].item2 == this.baseItems[index2].name) {
       this.items[index].item2Desc = this.baseItems[index2].description
       this.items[index].item2Img = this.baseItems[index2].image
     }
    } 
  }

}
}


</script>

<style scoped>
ul{
  list-style: none;
  padding: 0px;
}

input[type="radio"] {
  display: none;
}



label:before {
  background-color: white;
  color: white;
  content: " ";
  display: block;
  border-radius: 50%;
  border: 1px solid grey;
  position: relative;
  top: 20px;
  left: -5px;
  width: 25px;
  height: 25px;
  text-align: center;
  line-height: 28px;
  transition-duration: 0.4s;
  transform: scale(0);
}

:checked + label {
  border-color: rgb(233, 22, 15);
}

:checked + label:before {
  content: "✓";
  background-color: grey;
  transform: scale(1);
  z-index: 1;
}

:checked + label img {
  transform: scale(0.9);
  box-shadow: 0 0 5px rgb(226, 10, 10);
  z-index: -2;
}

li{
  display: inline-block;
  margin: 10px;
}

img{
  border-radius: 10px;
}

.container{
    margin-top: 50px;
    display: grid;
    justify-items: center;
    grid-gap: 20px;
    margin-left: 10px;
    margin-right: 10px;
}

.wynik{
  display: grid;
  grid-template-columns: 30px 64px 30px 64px 1fr;
  margin-left: 5px;
  margin-right: 5px;
  height: 80px;
  align-items: center;
}

span{
  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;
}

.itemName{
  margin: 5px;
  font-weight: bold;
  display: grid;
}

.itemDesc{
  display: grid;
  grid-template-columns: 1fr;
  font-size: 12px;
}

.desc{
  margin-left: 5px;
  margin-right: 5px;
  display: grid;
  align-items: center;
  text-align: center;
}
.item{
  box-shadow:   0px 7px 10px 0px rgba(0, 0, 0, 0.3);
  border-radius: 5px;
  
}

@media (max-width: 320px){
.item{
  width: 300px;
}
}
@media (min-width: 375px){
.item{
  width: 340px;
}
}
@media (min-width: 768px){
.item{
  width: 500px;
}
}


#symbol{
  font-size: 30px;
}

</style>

