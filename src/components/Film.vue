<template>
	<v-container>
		<v-row class="my-3">
			Film {{ $route.params.film }}
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "Film",
	props: {
		film: Number
	}
}
</script>

<style scoped>

</style>
