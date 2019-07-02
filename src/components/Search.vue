<template>
    <div class="SearchWrapper">
        <input type="text" name="search" id="search" placeholder="Infinity Edge" v-model="searchInput"  @input="handleInput" autocomplete="off" >
       
      <div class="container">
           <div v-for="item in results" class="wynik" :key="item.name">
            <div class="itemName">
              <div class="img"><img :src="item.image" :alt="item.name"></div><div><h3>{{ item.name }}</h3><p>{{item.description}}</p></div>
            </div>
           <div class="itemPart">
             <div  class="img"><img :src="item.item1Img" :title="item.item1Desc" :alt="item.item1"></div><p>{{item.item1}}</p>
             <div class="img"><img :src="item.item2Img" :title="item.item1Desc" :alt="item.item2"></div><p>{{item.item2}}</p>
             </div>
           </div>
      </div>
        
    </div>
</template>

<script>
import items from '../assets/items.json'
import baseItems from '../assets/baseItems.json'
import debounce from 'lodash.debounce'
export default {
    name: 'Search',

    data(){
  return{
    searchInput: '',
    results: [],
    items: items,
   baseItems: baseItems,

  
  };
},


methods: {
handleInput: debounce(function() {
  this.$emit('changed', '2')
    if (this.searchInput == "") {
      this.results.length = 0; 
    } else {
      let input = this.searchInput.toUpperCase()
    
    this.results.length = 0; 
  for (let index = 0; index <= this.items.length; index++) {
      let temp = this.items[index].name;
      let temp1 = this.items[index].item1.toUpperCase();
       let temp2 = this.items[index].item2.toUpperCase();
      temp = temp.toUpperCase(); 
     
     if (temp.includes(input) || temp1.includes(input) || temp2.includes(input) ) {
         this.results.push(this.items[index]);
         
     }    
  }
    }   
}, 500),



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

},

}
</script>

<style scoped>
input{
    margin-top: 30px;
    text-align: center;
    border: none;
    outline: none;
    border-bottom: 2px solid rgba(0, 0, 0, 0.637);
    font-size: 20px;
    padding: 10px;

}

input:focus{
    outline: none;
    box-shadow: 1px 15px 10px -10px rgba(0, 0, 0, 0.3)
}

@media (min-width: 768px) {
.container{
    display: grid;
     grid-template-columns: 1fr 1fr;
}
}

@media (min-width: 1024px) {
.container{
    display: grid;
     grid-template-columns: 1fr 1fr 1fr;
}
}
  
.container{
    margin-top: 50px;
    display: grid;
    grid-gap: 20px;
    margin-left: 10px;
    margin-right: 10px;
}

.wynik h3{
   font-size: 20px;
}
.wynik{
  box-shadow:   0px 7px 10px 0px rgba(0, 0, 0, 0.3);
  border-radius: 5px;
}
.itemName{
    display: inline-grid;
    grid-template-columns: 63px 1fr;
    width: 100%;
    margin-bottom: 15px;
    padding-left: 10px;
    padding-right: 10px;
}

.img{
    display: flex;
    align-items: center;
    
}

.itemPart{
  display: grid;
  grid-template-columns: 40px 1fr 40px 1fr;
  font-size: 12px;
  margin-bottom: 5px;
  padding-left: 10px;
  padding-right: 10px;
}

.itemPart img{
  max-width: 40px;
  height: auto;
  border-radius: 5px;
}

.itemName img{
  border-radius: 5px;
}

.itemName p{
font-size: 12px;
}
.itemName h3{
  margin-bottom: 0.5em;
  margin-top: 0.5em;
}

</style>
S