<template>

  <div class="randomizator">
		<div class="randomizator-text">{{beerCard.text}}</div>
		<div class="beer-card">
			<div class="beer-card__item beer-card__brand">{{beerCard.brand}}</div>
			<div class="beer-card__item beer-card__name">{{beerCard.name}}</div>
			<div class="beer-card__item beer-card__style">{{beerCard.style}}</div>
			<div class="beer-card__item beer-card__alcohol">{{beerCard.alcohol}}</div>
		</div>
		<button @click="fetchBeerData" class='randomizator__btn'>{{beerCard.btn}}</button>
	</div>

</template>

<script>
import axios from 'axios'

export default {
	data(){
		return{
			beerCard:{
				text: 'Choose your beer!',
				btn: 'Random beer!',
				brand: null,
				name: null,
				style: null,
				alcohol: null,
			}
		}
	},
	methods: {
		async fetchBeerData(){
			try{
				const url = 'https://random-data-api.com/api/beer/random_beer';
				const response = await axios.get(url)
				const beerData = response.data
				
				this.beerCard.text = 'Chosen one beer:',
				this.beerCard.btn = 'one more beer!',
				this.beerCard.brand = 'Brand: ' + beerData.brand,
				this.beerCard.name = 'Name: ' + beerData.name,
				this.beerCard.style = 'Style: ' + beerData.style,
				this.beerCard.alcohol = 'Alc: ' + beerData.alcohol
				
			} catch(e) {
				alert(e)
			}
		},
	}
}
</script>

<style scoped>

.randomizator {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	row-gap: 20px;
	flex: 1 1 50%;
		
}
.randomizator-text{
	color: #35495E;
	font-size: 30px;

}

.randomizator__btn{
	margin-top: 10px;
	padding: 10px 30px;
	border-radius: 45px;
	color: #ffffff;
	text-align: right;
	font-size: 20px;
	background: #35495E;
	transition: 0.2s all;
}

.randomizator__btn:hover{
	color: #ffffff;
	background: #42B983;
}

.beer-card__item{
	font-size: 20px;
	margin-top: 10px;
}



</style>