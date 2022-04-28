<template>
	<button class="btn">
		<slot></slot>
	</button>
</template>

<script>
export default {

}
</script>

<style scoped>
.btn{
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
</style>