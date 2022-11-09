<template>
	<q-page class="flex flex-center">
		<q-card class="q-ma-sm column items-center" flat bordered v-for="(name, index) in pkmList" :key="index">
			<q-toolbar class="bg-accent text-white text-center text-capitalize">
				<q-toolbar-title>
					{{ pkmList[index].name }}
				</q-toolbar-title>
			</q-toolbar>
			<q-card-section>
				<div>
					{{ pkmDetail }}
				</div>
			</q-card-section>
		</q-card>
	</q-page>
</template>

<style>

</style>

<script>
import axios from "axios";

export default {
	name: "ListPkm",
	data() {
		return {
			pkmList: [],
			pkmDetail: [],
		};
	},
	created() {
		axios
			.get(`https://pokeapi.co/api/v2/pokemon/`)
			.then((pkm) => {
				this.pkmList = pkm.data.results;
			})
			.catch((error) => console.log(error));
	},
	// methods: {
	// 	getPkmDetails(url) {
	// 		axios
	// 			.get(url)
	// 			.then((pkm) => {
	// 				this.pkmDetail = pkm.data;
	// 			})
	// 			.catch((error) => console.log(error));
	// 	},
	// },
	watch: {
		pkmList(newValue, oldValue) {
			console.log(newValue);
			console.log(oldValue);
			axios
				.get(newValue.url)
				.then((pkm) => {
					this.pkmDetail = pkm.data;
					console.log(this.pkmDetail);
				})
				.catch((error) => console.log(error));
		}
	}
};
</script>
