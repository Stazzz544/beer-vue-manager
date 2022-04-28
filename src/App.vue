<template>
<div class="App">
	
	<header class="header">
		<div class="container">
			<h1 class="header__title" >Social beer network!</h1>
			<h2 class="header__subtitle">find your best beer!</h2>
		</div>
	</header>


	<main class="main">
		<div class="container">
			<div class="profile">
				<div class="user">
					<div class="user__photo-wrapper-outside">
						<div class="user__photo-wrapper-inside">
							<img :src="userData.avatar" alt="" class="user__photo-img">
						</div>
					</div>

					<div class="user__info-wrapper">
						<div class="user__info">Name: {{userData.firstName}}</div>
						<div class="user__info">Surname: {{userData.lastName}}</div>
						<div class="user__info">Age: {{userData.fullYears}}</div>
						<div class="user__info">Work as: {{userData.employment}}</div>
					</div>

				</div>

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
			</div>	
		</div>
	</main>

	<footer class="footer">
		<div class="footer__copyright">© 2022 Stanislav Vasilev</div>
	</footer>
</div>
</template>

<script>
import axios from 'axios'

export default {
	data(){
		return{
			userData:{
				avatar: null,
				firstName: null,
				lastName: null,
				fullYears: null,
				employment: null,
			},
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
		async fetchUser() {
			try{
				const url = 'https://random-data-api.com/api/users/random_user'
				const response = await axios.get(url)
				const userData = response.data

				if (userData.date_of_birth){
					const arr = userData.date_of_birth.split('-')
					const userBerthday = new Date(+arr[0], arr[1], +arr[2])
					const today = (Date.now() - userBerthday)
					this.userData.fullYears = Math.floor(today / (1000 * 60 * 60 * 24 * 30 * 12))
				} else {
					return 'no information'
				}

				this.userData.avatar = userData.avatar
				this.userData.firstName = userData.first_name
				this.userData.lastName = userData.last_name
				this.userData.employment = userData.employment.title
			} catch (e) {
				alert(e)
			}
		},
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
	},
	
	beforeMount(){
		this.fetchUser()
	},
	
}
</script>

<style>
/*------reset styles start-------*/
* {
	padding: 0;
	margin : 0;
	border : 0;
}

*,
*:before,
*:after {
	-webkit-box-sizing: border-box;
	box-sizing        : border-box;
}

:focus,
:active {
	outline: none;
}

a:focus,
a:active {
	outline: none;
}

nav,
footer,
header,
aside {
	display: block;
}

html,
body {
	height                  : 100%;
	width                   : 100%;
	font-size               : 100%;
	line-height             : 1;
	font-size               : 14px;
	-ms-text-size-adjust    : 100%;
	-moz-text-size-adjust   : 100%;
	-webkit-text-size-adjust: 100%;
	font-family:monospace
}

input,
button,
textarea {
	font-family: inherit;
}

input::-ms-clear {
	display: none;
}

button {
	cursor: pointer;
}

button::-moz-focus-inner {
	padding: 0;
	border : 0;
}

a,
a:visited {
	text-decoration: none;
}

a:hover {
	text-decoration: none;
}

ul li {
	list-style: none;
}

img {
	vertical-align: top;
}

h1,
h2,
h3,
h4,
h5,
h6 {
	font-size  : inherit;
	font-weight: inherit;
}

/*------reset styles end-------*/


/* header */

.header{
	color: #ffffff;
	text-align: right;
	font-size: 20px;
	height: 60px;
	background: #35495E
}

.header__title{
	margin-top: 7px;
	margin-right: 10%;
	letter-spacing: 6px;
}

.header__subtitle{
	margin-top: 4px;
	letter-spacing: 3px;
}

/* main */
.main{
	flex: 1 1
}

/* user section */
.App{
	height: 100vh;
	background: #42B983;
	display: flex;
	flex-direction: column;
}

.container {
	max-width: 800px;
	margin: 0 auto;
}

.main > .container {
	background: rgb(255, 255, 255);
	height: 100%;
}

.profile {
	display: flex;
	padding: 30px 40px;
}

.randomizator {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: space-around;
	flex: 1 1 50%;
		
}
.randomizator-text{
	color: #35495E;
	font-size: 30px;

}

.randomizator__btn{
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

.user{
	flex: 1 1 50%;
}

.user__photo-wrapper-outside {
	width: 200px;
	height: 200px;
	border-radius: 50%;
	border: solid 3px #42B983;
}

.user__photo-wrapper-inside {
	border-radius: 50%;
	border: solid 6px rgb(215, 215, 255);
	width: 195px;
	height: 195px;
	overflow: hidden;
}

.user__photo-img {
	width: 100%;
	height: 100%;
	object-fit: cover;
	background: #42B983;
}

.user__info-wrapper {
	margin-top: 30px;
}

.user__info {
	margin-top: 5px;
	color: #35495E;
	font-size: 18px;
	font-weight: 700;
}

/* beerCard */
.beer-card{
}

.beer-card__item{
	font-size: 20px;
	margin-top: 10px;
}


/* footer */

.footer{

}

.footer__copyright{
	text-align: center;
	font-size: 20px;
	line-height: 40px;
	color: #ffffff;
	height: 40px;
   background: #35495E
}

</style>

