<template>
  <div class="user__photo-wrapper-outside">
		<div  class="user__photo-wrapper-inside">
			<div :class=loading>loading...</div> 
			<img :src="userData.avatar" alt="" :class=avatar>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		userData: {
			type: Array,
			required: true,
		}
	},
	data(){
		return {
			loading: 'spinner active ',
			avatar: 'user__photo-img'
		}
	},
	methods: {
		loader() {
			if (this.userData.loader) {
				this.loading = 'loading active '
			} else {
				this.loading = 'loading'; 
				this.avatar = 'user__photo-img active';
			} 
		},
	},
	beforeMount(){
		this.loader()
	},
	updated(){
		this.loader()
	}
}
</script>


<style>
.loading{
	display: none;
	width: 105%;
	height: 105%;
	object-fit: cover;
	background: #42B983;
	justify-content: space-around;
   align-items: center;
   font-size: 25px;
	animation: infinite 1s pulse ease-in;
}
.loading.active{
	display: flex;
}

.user__photo-wrapper-outside {
	width: 200px;
	height: 200px;
	border-radius: 50%;
	border: solid 3px #42B983;
}

.user__photo-wrapper-inside {
	position: relative;
	border-radius: 50%;
	border: solid 6px rgb(215, 215, 255);
	width: 195px;
	height: 195px;
	overflow: hidden;
}

.user__photo-img {
	display: none;
	width: 110%;
	height: 110%;
	object-fit: cover;
	background: #42B983;
	transform: translateY(-3px) translateX(-3px);
}

.user__photo-img.active {
	display: block;
}

@keyframes pulse {
	0% {transform: scale(1)}
	50% {transform: scale(1.1)}
	100% {transform: scale(1)}
}

</style>