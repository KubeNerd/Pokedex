<template>
		<div  class="container" id="pokemon">
			<div class="card">
				<div class="card-body">
					<img class="card-img-top" :src="currentImg" alt="Card image cap" style="width:100px">
					<h5 class="card-title">{{ name | upper }} - {{ num  + 1}}</h5>
					<p class="card-text">{{ pokemon.type }}</p>
					<div>
						<button type="button" class="btn btn-info btn-block" @click="mudarSprite">Mudar Sprite</button>
					</div>
				</div>
			</div>
  </div>
</template>

<script>
import axios from "axios";
export default {
	created:function(){ 
		axios.get(this.url)
			.then(res =>{
				this.pokemon.type = res.data.types[0].type.name;
				this.pokemon.front = res.data.sprites.front_default;
				this.pokemon.back = res.data.sprites.back_default;
				this.currentImg = this.pokemon.front;
	
				console.log(this.pokemon)
			}).catch(err =>{
				console.log(err)
			})
	},
	data(){
		return{
			isFront:true,
			currentImg:"",
			pokemon:{
				type:"",
				front:"",
				back:""
			}
		}
	},
	name:"Pokemon",
	props: {
		num:Number,
		name:String,
		url:String
	},
	filters:{
		upper:function(value){
			const newname = value[0].toUpperCase() + value.slice(1);
			return newname;
		}
	},
	methods:{
		mudarSprite:function(){
			if(this.isFront){
				this.isFront = false
				this.currentImg = this.pokemon.back
			} else {
				this.isFront = true;
				this.currentImg = this.pokemon.front;
			}
		}
	}
}
</script>


<style scoped>
	#pokemon{
		margin-top: 2%;
	}
</style>
