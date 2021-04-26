<template>
	<div id="app">
		<div class="container">
			<img src="./assets/guia_pokex.png">
			<hr/>
			<h3>Pokedex - Guia Do Programador - Formação Node.js </h3>
			<hr/>
			<div>
				<input class="form-control"  type="text"  placeholder="Buscar pokemon pelo nome" v-model="busca" style="border-radius:100px"><br/>
				<button class="btn btn-primary" id="buscaBtn" @click="buscar">Buscar</button>
			</div>

			<div v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url">
				<Pokemon :name="pokemon.name" :url="pokemon.url" :num="index"/>
			</div>
		</div>
	</div>
</template>

<script>
import Pokemon from "./components/Pokemon";
import "bootstrap/dist/css/bootstrap.css";
import axios from "axios";


export default {
	name: "App",
	data(){
		return {
			pokemons:{},
			filteredPokemons: [],
			busca:""
		}
	},

	created:function(){
		axios.get("https://pokeapi.co/api/v2/pokemon?offset=100&limit=100")
			.then(( res ) =>{
				this.pokemons = res.data.results
			})
	},
	components:{
		Pokemon
	},
	computed:{ 
		// resultadoBusca:function(){
		// 	if(this.busca == "" || this.busca == " "){
		// 		return this.pokemons;
		// 	} else {
		// 		return this.pokemons
		// 	}
		// }
	},
	methods:{
		buscar:function(){
			if(this.busca.length <= 0 || this.busca.length == ""){
				console.log("busca vazia mano", this.busca)
				return this.filteredPokemons = this.pokemons;
			} else {
				this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
			}
		}
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
</style>
