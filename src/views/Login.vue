<template>
	<v-container>
		<v-row justify="space-between">
			<v-col>
				<form>
					<v-text-field sm="12" md="6" lg="4" xl="3" v-model="input.user" :counter="max" label="Username"></v-text-field>
					<v-text-field sm="12" md="6" lg="4" xl="3" v-model="input.pass" :counter="max" label="Password" type="password"></v-text-field>
					<v-btn v-on:click="login()" block>Login</v-btn>
				</form>
			</v-col>
		</v-row>
	</v-container>
</template>

<style scoped>

</style>

<script>
import axios from 'axios';
export default {
	data: () => ({
		input: {
			user: '',
			pass: '',
		},
		max: 6,
		model: 'Foobar',
	}),

	computed: {

	},

	methods: {
		login() {
			let form_data = new FormData();
			form_data.append('user', this.input.user);
			form_data.append('pass', this.input.pass);
			const headers = {
				'Content-Type': 'application/x-www-form-urlencoded'
			};

			axios.post('http://www.pliassas.gr/test/check.php', form_data, { headers })
			.then( r => {
				console.log(r.data);
			});
		}
	}
}
</script>
