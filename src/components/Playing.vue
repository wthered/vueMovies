<template>
	<v-container>
		<v-row id="title">
			Now Playing
			<v-spacer></v-spacer>
			Show More
			<v-btn icon>
				<v-icon>mdi-dots-vertical</v-icon>
			</v-btn>
		</v-row>
		<v-row class="text-center">
			<v-col v-for="play in playing" v-bind:key="play.id" cols="3">
				<v-card>
					<v-img
						:src="'https://image.tmdb.org/t/p/original' + play.backdrop_path"
						class="white--text align-end"
						gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)">
						<v-card-title v-text="play.title"></v-card-title>
					</v-img>
					<v-card-actions>
						<v-spacer></v-spacer>

						<v-btn icon>
							<v-icon>mdi-heart</v-icon>
						</v-btn>

						<v-btn icon>
							<v-icon>mdi-bookmark</v-icon>
						</v-btn>

						<v-btn icon>
							<v-icon>mdi-share-variant</v-icon>
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-col>
		</v-row>
  </v-container>
</template>

<style scoped>
#title {
	line-height: 1rem;
	color: red;
	font-size: 3rem;
	padding-bottom: 1rem;
	letter-spacing: 1px;
	font-family: "Roboto", sans-serif;
}
</style>
<script>
import axios from 'axios';
export default {
	name: 'HelloWorld',

	data: () => ({
		playing: null
	}),
	async created() {
		await axios.get("https://api.themoviedb.org/3/movie/now_playing?api_key=1cd7d832933a3f8cb0c956ac70964e5f&language=en-US&page=1")
			.then((response) => {
				this.playing = response.data.results;
			});
	}
}
</script>
