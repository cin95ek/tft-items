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

import debounce from 'lodash.debounce'
export default {
    name: 'Search',

    data(){
  return{
    searchInput: '',
    results: [],
    items: [
     
    {"name":"Blade of the Ruined King", "description":"Wearer is also a Blademaster.", "item1":"Spatula", "item2":"Recurve Bow", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3153.png"}, 
    {"name":"Bloodthirster", "description":"35% Lifesteal", "item1":"B.F. Sword", "item2":"Negatron Cloak", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3072.png"}, 
    {"name":"Brawler's Gloves", "description":"Wearer is also a Brawler.", "item1":"Spatula", "item2":"Negatron Cloak", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/1051.png"}, 
    {"name":"Cursed Blade", "description":"Attacks have a low chance to Reduce enemy's star level by 1", "item1":"Negatron Cloak", "item2":"Recurve Bow", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3137.png"}, 
    {"name":"Darkin", "description":"Wearer is also a Demon.", "item1":"Spatula", "item2":"Tear of the Goddess", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/spell/AatroxR.png"}, 
    {"name":"Dragon's Claw", "description":"Gain 83% resistance to magic damage.", "item1":"Negatron Cloak", "item2":"Negatron Cloak", "image":"https://mruszkiewicz.pl/img/DragonsClaw.png"}, 
    {"name":"Force of Nature", "description":"Gain 1+ Team Size", "item1":"Spatula", "item2":"Spatula", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/4401.png"}, 
    {"name":"Frozen Heart", "description":"Adjacent enemies Attack Speed is 20% Slower.", "item1":"Tear of the Goddess", "item2":"Chain Vest", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3110.png"}, 
    {"name":"Frozen Mallet", "description":"Wearer is also a Glacial.", "item1":"Spatula", "item2":"Giant`s Belt", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3022.png"}, 
    {"name":"Guardian Angel", "description":"Wearer revives with 500 Health.", "item1":"B.F. Sword", "item2":"Chain Vest", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3026.png"}, 
    {"name":"Guinsoo's Rageblade", "description":"Attacks grant 3% Attack Speed. Stacks infinitely.", "item1":"Recurve Bow", "item2":"Needlessy Large Rod", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3124.png"}, 
    {"name":"Hextech Gunblade", "description":"Heal for 25% of all damage dealt.", "item1":"B.F. Sword", "item2":"Needlessy Large Rod", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3146.png"}, 
    {"name":"Hush", "description":"Attacks have a high chance to Silence.", "item1":"Negatron Cloak", "item2":"Tear of the Goddess", "image":"https://mruszkiewicz.pl/img/Hush.png"}, 
    {"name":"Infinity Edge", "description":"Critical Strikes deal +100% damage.", "item1":"B.F. Sword", "item2":"B.F. Sword", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3031.png"}, 
    {"name":"Ionic Spark", "description":"Whenever an enemy casts a spell, they take 200 damage.", "item1":"Negatron Cloak", "item2":"Needlessy Large Rod", "image":"https://mruszkiewicz.pl/img/IonicSpark.png"}, 
    {"name":"Knight's Vow", "description":"Wearer is also a Knight.", "item1":"Spatula", "item2":"Chain Vest", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3109.png"}, 
    {"name":"Locket of the Iron Solari", "description":"On start of combat, all adjacent allies gain a shield of 200.", "item1":"Chain Vest", "item2":"Needlessy Large Rod", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3190.png"}, 
    {"name":"Luden's Echo", "description":"Spells deal 200 splash damage on hit.", "item1":"Needlessy Large Rod", "item2":"Tear of the Goddess", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3285.png"}, 
    {"name":"Morellonomicon", "description":"Spells deal burn damage equal to 10% of the enemy's maximum health per second.", "item1":"Needlessy Large Rod", "item2":"Giant`s Belt", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3165.png"}, 
    {"name":"Phantom Dancer", "description":"Wearer dodges all Critical Strikes.", "item1":"Chain Vest", "item2":"Recurve Bow", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3046.png"}, 
    {"name":"Rabadon's Deathcap", "description":"Spell Damage +50% AP", "item1":"Needlessy Large Rod", "item2":"Needlessy Large Rod", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3089.png"}, 
    {"name":"Rapid Firecannon", "description":"Wearer's attacks cannot be dodged. Attack Range is doubled.", "item1":"Recurve Bow", "item2":"Recurve Bow", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3094.png"}, 
    {"name":"Red Buff", "description":"Attacks deal 2.5% Maximum Health burn damage. Burned units cannot heal.", "item1":"Chain Vest", "item2":"Giant`s Belt", "image":"https://mruszkiewicz.pl/img/RedBuff.png"}, 
    {"name":"Redemption", "description":"On death, heal all nearby allies for 1000 Health.", "item1":"Giant`s Belt", "item2":"Tear of the Goddess", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3107.png"}, 
    {"name":"Runaan's Hurricane", "description":"Attacks 2 additional enemies. These additional attacks deal 50% damage.", "item1":"Negatron Cloak", "item2":"Spatula", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3085.png"}, 
    {"name":"Seraph's Embrace", "description":"Regain 20 mana each time a spell is cast", "item1":"Tear of the Goddess", "item2":"Tear of the Goddess", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3040.png"}, 
    {"name":"Spear of Shojin", "description":"After casting an ability, wearer gains 15% of its max mana per attack", "item1":"B.F. Sword", "item2":"Tear of the Goddess", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3161.png"}, 
    {"name":"Statikk Shiv", "description":"Every 3rd attack deals 100 splash magical damage.", "item1":"Recurve Bow", "item2":"Tear of the Goddess", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3087.png"}, 
    {"name":"Sword Breaker", "description":"Attacks have a chance to disarm.", "item1":"Chain Vest", "item2":"Negatron Cloak", "image":"https://mruszkiewicz.pl/img/SwordBreaker.png"}, 
    {"name":"Sword of the Divine", "description":"Each second, the wearer has a 5% chance to gain 100% Critical Strike.", "item1":"B.F. Sword", "item2":"Recurve Bow", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3131.png"}, 
    {"name":"Thornmail", "description":"Reflect 35% of damage taken from attacks.", "item1":"Chain Vest", "item2":"Chain Vest", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3075.png"}, 
    {"name":"Titanic Hydra", "description":"Attacks deal 10% of the wearer's max Health as splash damage.", "item1":"Giant`s Belt", "item2":"Recurve Bow", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3748.png"}, 
    {"name":"Warmog's Armor", "description":"Wearer regenerates 3% max Health per second.", "item1":"Giant`s Belt", "item2":"Giant`s Belt", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3083.png"}, 
    {"name":"Youmuu's Ghostblade", "description":"Wearer is also an Assassin.", "item1":"Spatula", "item2":"B.F. Sword", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3142.png"}, 
    {"name":"Yuumi", "description":"Wearer is also a Sorcerer.", "item1":"Spatula", "item2":"Needlessy Large Rod", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/spell/YuumiW.png"}, 
    {"name":"Zeke's Herald", "description":"Adjacent allies gain +10% Attack Speed.", "item1":"B.F. Sword", "item2":"Giant`s Belt", "image":"https://mruszkiewicz.pl/img/ZekesHerald.png"}, 
    {"name":"Zephyr", "description":"On start of combat, banish an enemy for 5 seconds.", "item1":"Giant`s Belt", "item2":"Negatron Cloak", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3172.png"}
  ],
   baseItems: [
     
    {"name":"B.F. Sword", "description":"20 Attack Damage.", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/1038.png"}, 
    {"name":"Recurve Bow", "description":"20% Attack Speed.", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/1043.png"}, 
    {"name":"Chain Vest", "description":"20 Armor.", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/1031.png"}, 
    {"name":"Negatron Cloak", "description":"20 Magic Resist.", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/1057.png"}, 
    {"name":"Needlessy Large Rod", "description":"20% Spell Damage.", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/1058.png"}, 
    {"name":"Tear of the Goddess", "description":"20 Starting Mana.", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/3070.png"}, 
    {"name":"Giant`s Belt", "description":"200 Health", "image":"https://ddragon.leagueoflegends.com/cdn/9.13.1/img/item/1011.png"}, 
    {"name":"Spatula", "description":"Use to craft special items.", "image":"https://mruszkiewicz.pl/img/spatula.png"},
    
  ],

  
  };
},


methods: {
handleInput: debounce(function() {
  this.$emit('changed', '1')
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