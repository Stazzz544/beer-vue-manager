<template>
<div class="App">
	<Header/>

	<main class="main">
		<div class="container">
			<div class="profile">
				<UserProfile/>
				<Randomizator/>
			</div>	
		</div>
	</main>

	<Footer/>
</div>
</template>

<script>
import Header from '@/components/Header.vue'
import UserProfile from '@/components/UserData/UserProfile.vue'
import Footer from '@/components/Footer.vue'
import Randomizator from '@/components/Randomizator/Randomizator.vue'

export default {
	components:{
		Header,
		Footer,
		Randomizator,
		UserProfile,
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

/* main */
.main{
	flex: 1 1;
	display: flex;
	flex-direction: column;
	padding: 0 20px;
}

/* user section */
.App{
	min-height: 100vh;
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
	flex: 1 1
}

.profile {
	display: flex;
	padding: 30px 40px;
}

/* =======all medias======== */
@media(max-width: 645px) {
	.profile{
		flex-direction: column;
		row-gap: 40px;
	}
	.user{
		display: flex;
		column-gap: 20px;
	}
	.randomizator{
		row-gap: 40px;
	}
}

@media(max-width: 480px) {
	.user {
		flex-direction: column;
		align-items: center;
	}
	.main{
		padding: 0;
	}
}



</style>

