<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h4 class="is-size-4">Pokedex</h4>
      <input class="input is-rounded" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca">
      <button id="busca-btn" class="button is-fullwidth button is-success" @click="buscar">Buscar</button>
        <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
    </div>  
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon"

export default {
  name: 'App',
  data(){

    return{
      pokemons:[],
      busca: "",
      filteredPokemons:[],
    }
  },
  created:function (){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((data) =>{
      this.pokemons = data.data.results;
      this.filteredPokemons = data.data.results;
    })
  },
  components:{
    Pokemon
  },

methods:{
  buscar: function(){
    var newBusca = this.busca;
    newBusca = newBusca.toLowerCase();
    
    this.filteredPokemons = this.pokemons;

    if(newBusca == "" || newBusca == " "){
      this.filteredPokemons = this.pokemons
  
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemons => pokemons.name == newBusca);
      }
  }
},

  computed:{
    /*resultadoBusca: function(){
      if(this.busca == "" || this.busca == " "){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }*/
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#busca-btn{
  margin-top:3%;

}
</style>
