<template>
<div class="user">
	<UserAvatar :userData = 'userData'/>
	<UserInfo :userData = 'userData'/>
</div>
</template>

<script>
import axios from 'axios'
import UserInfo from '@/components/UserData/UserInfo.vue'
import UserAvatar from '@/components/UserData/UserAvatar.vue'

export default {
	data(){
		return{
			userData:{
				avatarStatus: null,
				firstName: null,
				lastName: null,
				fullYears: null,
				employment: null,
				avatarUrl: null,
				avatar: null,
				loader: true
			},
			userAvatar:{}
		}
	},
	components: {
		UserInfo,
		UserAvatar,
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

				this.userData.avatarUrl = userData.avatar
				this.userData.firstName = userData.first_name
				this.userData.lastName = userData.last_name
				this.userData.employment = userData.employment.title
				this.fetchAvatar()
			} catch (e) {
				alert(e)
			}
		},
		async fetchAvatar() {
			try {
				const url = this.userData.avatarUrl;
				await axios.get(url)
				this.userData.avatar = url
				this.userData.loader = false
			} catch (e) {
				this.fetchAvatar()
			}
		}
	},
	beforeMount(){
		this.fetchUser()
	},
}
</script>

<style scoped>

.user{
	flex: 1 1 50%;
}
</style>