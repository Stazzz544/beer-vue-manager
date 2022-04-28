<template>
<div class="user">
	<UserAvatar :userAvatar = 'userAvatar'/>
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
				firstName: null,
				lastName: null,
				fullYears: null,
				employment: null,
			},
			userAvatar:{
				avatarStatus: null,
				avatarUrl: null,
				avatar: null,
				loader: true
			}
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
				const responseUserData = response.data

				if (responseUserData.date_of_birth){
					const arr = responseUserData.date_of_birth.split('-')
					const userBerthday = new Date(+arr[0], arr[1], +arr[2])
					const today = (Date.now() - userBerthday)
					this.userData.fullYears = Math.floor(today / (1000 * 60 * 60 * 24 * 30 * 12))
				} else {
					return 'no information'
				}

				this.userAvatar.avatarUrl = responseUserData.avatar
				this.userData.firstName = responseUserData.first_name
				this.userData.lastName = responseUserData.last_name
				this.userData.employment = responseUserData.employment.title
				this.fetchAvatar()
			} catch (e) {
				alert(e)
			}
		},
		async fetchAvatar() {
			try {
				const url = this.userAvatar.avatarUrl;
				await axios.get(url)
				this.userAvatar.avatar = url
				this.userAvatar.loader = false
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