<template>
	<v-autocomplete
			v-model="friends"
			:disabled="isUpdating"
			:items="people"
			filled
			label="Search Film Title"
			item-text="title"
			item-value="movie_id"
			:loading="loading"
			:search-input.sync="search"
			cache-items
			class="mx-4"
			flat
			hide-no-data
			hide-details
	>
		<template v-slot:selection="data"><span id="result">{{ data.item.title }}</span></template>
		<template v-slot:item="data">
			<template v-if="typeof data.item !== 'object'">
				<v-list-item-content v-text="data.item"></v-list-item-content>
			</template>
			<template v-else>
				<v-list-item-avatar>
					<img :src="data.item.poster" :alt="'Avatar of ' + data.item.title">
				</v-list-item-avatar>
				<v-list-item-content>
					<v-list-item-title v-html="data.item.title"></v-list-item-title>
					<v-list-item-subtitle v-html="data.item.released"></v-list-item-subtitle>
				</v-list-item-content>
			</template>
		</template>
	</v-autocomplete>
</template>

<script>
// import axios from 'axios';
import axios from "axios";

export default {
	name: "SearchBar",

	data () {
		return {
			loading: false,
			items: [],
			search: null,
			select: null,
			friends: [],
			isUpdating: false,
			people: [
				// { header: 'Group 1' },
				// {movie_id:1,title:"The Lone Ranger",poster:"https://image.tmdb.org/t/p/original/b2je2ZybNIzAOL1K1WPbbT6zt2M.jpg",released: "1980-09-15"},
				// {movie_id:2,title:"Dark Shadows",poster:"https://image.tmdb.org/t/p/original/eteQ3gyMpA0oiWcYX4XoXGry0cB.jpg",released: "1980-09-15"},
				// {movie_id:3,title:"The Rum Diary",poster:"https://image.tmdb.org/t/p/original/8xmzSn5Qd3lX9iqrkoY27wMRE3O.jpg",released: "1980-09-15"},
				// {movie_id:4,title:"Rango",poster:"https://image.tmdb.org/t/p/original/m5kz9dXHhAqzxknwuACvcgJmQSH.jpg",released: "1980-09-15"},
				// {movie_id:5,title:"Abigail",poster:"https://image.tmdb.org/t/p/original/3rNWxdsUYDsDxHrEc3OmXZVdKwJ.jpg",released: "1980-09-15"},
				// { divider: true },
				// { header: 'Group 2' },
				// {movie_id:6,title:"Viva the Underdogs",poster:"https://image.tmdb.org/t/p/original/g2PhWNQzwmJhIkoN1WmQ9O7ZAS9.jpg",released: "1980-09-15"},
				// {movie_id:7,title:"Black and Blue",poster:"https://image.tmdb.org/t/p/original/1cSHEKYYP8Dpi4o1iBVd4U75FYt.jpg",released: "1980-09-15"},
				// {movie_id:8,title:"Iranian Movie 2",poster:"https://image.tmdb.org/t/p/original/79i6vPlbretCusDSevWgNCe5BD3.jpg",released: "1980-09-15"},
				// {movie_id:9,title:"Alice in Wonderland",poster:"https://image.tmdb.org/t/p/original/o0kre9wRCZz3jjSjaru7QU0UtFz.jpg",released: "1980-09-15"},
				// {movie_id:10,title:"Public Enemies",poster:"https://image.tmdb.org/t/p/original/3KgtekisQBrHRsm2cD5UOB6Ce3k.jpg",released: "1980-09-15"}
			],
		}
	},
	watch: {
		isUpdating (val) {
			if (val) {
				setTimeout(() => (this.isUpdating = false), 500)
			}
		},

		async search (val) {
			let form_data = new FormData();
			form_data.append('film', val);
			const headers = {
				'Content-Type': 'application/x-www-form-urlencoded'
			};

			axios.post('http://www.pliassas.gr/movies/search.php', form_data, { headers })
				.then( r => {
					// console.log(r.data);
					this.people = r.data;
				})
			.then( () => {
				val && val !== this.select && this.querySelections(val);
			})
		},

		friends (newSelectedItem) {
			this.$router.push({ name: 'UserPage', params: { user: newSelectedItem } })
		},
	},
	methods: {
		async querySelections (v) {
			this.loading = true;
			// Simulated ajax query
			setTimeout(() => {
				this.people = this.people.filter(e => {
					return (e.title || '').toLowerCase().indexOf((v.title || '').toLowerCase()) > -1
				})
				this.loading = false;
			}, 500);
			console.log(v);
		},
	},
}
</script>

<style scoped>
#result {
	font-family: "Roboto", sans-serif;
	font-size: 1rem;
	color: #2c3e50;
}
</style>
