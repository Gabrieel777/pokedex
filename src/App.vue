<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h3 class="is-size-3">Pokedex</h3>

      <input type="text" class="input is-rounded" id="buscaBtn" placeholder="Encontrar pokemon pelo nome" v-model="busca"><br>
      <br> 
      <button class="button is-fullwidth is-success" @click="buscar">Encontrar</button>
      <br>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
      
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>

      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: async function(){
    let res = await axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0");
    this.pokemons = res.data.results;
    this.filteredPokemons = res.data.results;
  }, 
    components: {
      Pokemon  
  }, methods: {
      buscar: function(){
        this.filteredPokemons = this.pokemons;
        if(this.busca == "" || this.busca == " "){
          this.filteredPokemons = this.pokemons;
        } else {
          this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
        }
      }
  }, computed: {
  //   resultadoBusca: function(){
  //     if(this.busca == "" || this.busca == " "){
  //       return this.pokemons;
  //     } else {
  //       return this.pokemons.filter(pokemon => pokemon.name == this.busca);
  //     }
  //   }
  }
}

</script>

<style>

#buscaBtn {
  margin-top: 2%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>

