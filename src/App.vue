<template>
	<v-app>
		<v-card color="grey lighten-4" flat tile>
			<v-toolbar>
				<v-toolbar-title><a href="/" id="root">Film Base</a></v-toolbar-title>

				<v-spacer></v-spacer>

				<search-bar />

				<v-spacer></v-spacer>

				<v-btn class="mr-4" color="primary" dark to="/sign-in">
					<v-icon>mdi-account</v-icon>Login
				</v-btn>

				<v-btn class="ml-4" color="primary" dark to="/sign-up">
					<v-icon>mdi-account-plus</v-icon>
					Register
				</v-btn>
			</v-toolbar>
		</v-card>

		<v-main>
			<router-view></router-view>
		</v-main>

		<v-footer>
			Footer
		</v-footer>
	</v-app>
</template>

<style scoped>
a {
	text-decoration: none;
	font-family: "Roboto", sans-serif;
	font-size: 1.25rem;
	color: indianred;
}
</style>

<script>
import SearchBar from "@/views/SearchBar";

export default {
	name: 'App',

	components: {
		SearchBar,
	},

	data: () => ({

	}),
};
</script>
