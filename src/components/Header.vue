<template>
  <header class="header">
		<div class="container">
			<h1 class="header__title" >Social beer network!</h1>
			<h2 class="header__subtitle">find your best beer!</h2>
		</div>
	</header>
</template>

<script>
export default {
	
}
</script>

<style scoped>
	.header{
		color: #ffffff;
		text-align: right;
		font-size: 20px;
		min-height: 60px;
		background: #35495E;
		padding: 10px 5px;
	}

	.header__title{
		margin-top: 7px;
		margin-right: 10%;
		letter-spacing: 6px;
	}

	.header__subtitle{
		margin-top: 4px;
		margin-right: 5px;
		letter-spacing: 3px;
	}

@media(max-width: 550px) {
	.header__title{
		margin-right: 0;
	}
}

@media(max-width: 385px) {
	.header__title{
		line-height: 23px;
	}
}
</style>