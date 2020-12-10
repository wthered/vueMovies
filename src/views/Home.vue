<template>
	<v-container>
		<v-container class="home">
			<Playing/>
		</v-container>
		<v-container class="home">
			<Popular/>
			<Top/>
		</v-container>
	</v-container>
</template>

<script>
// @ is an alias to /src
import Playing from "@/components/Playing";
import Popular from "@/views/Popular";
import Top from "@/views/Top";


export default {
	name: 'Home',
	components: {
		Top,
		Popular,
		Playing
	}
}
</script>

<style scoped>
.home {
	background-color: #008B8B;
	border-radius: .5rem;
	border: 1px solid darkcyan;
	margin-top: 1rem;
}
</style>
