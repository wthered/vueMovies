<template>
	<v-container>
		<v-row class="my-3">
			User {{ $route.params.user }}
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "UserPage",
	props: {
		user: Number
	}
}
</script>

<style scoped>

</style>
