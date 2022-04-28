<template>
  <div class="user__info-wrapper">
		<div class="user__info">Name: {{userData.firstName}}</div>
		<div class="user__info">Surname: {{userData.lastName}}</div>
		<div class="user__info">Age: {{userData.fullYears}}</div>
		<div class="user__info">Work as: {{userData.employment}}</div>
	</div>
</template>

<script>
export default {
	props: {
		userData: {
			type: Array,
			required: true,
		}
	}
}
</script>

<style scoped>
.user__info-wrapper {
	margin-top: 30px;
}

.user__info {
	margin-top: 5px;
	color: #35495E;
	font-size: 18px;
	font-weight: 700;
	line-height: 22px;
}
</style>