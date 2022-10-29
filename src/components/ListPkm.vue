<template>
	<q-page class="flex flex-center">
		<q-card class="q-ma-sm" flat bordered v-for="(name, index) in pkmList" :key="index" >
			<q-toolbar class="bg-primary text-white text-capitalize" >
                    {{ pkmList[index].name }}
			</q-toolbar>
            <q-card-section>
				<div>
                    {{ pkmList[index].url }}
				</div>
            </q-card-section>
		</q-card>
	</q-page>
</template>

<style></style>

<script>
import axios from "axios";

export default {
	name: "ListPkm",
	data() {
		return {
			pkmList: [],
			pkmDetail: []
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
	methods: {
		getPkmDetails(url) {
			axios
				.get(url)
				.then((pkm) => {
					this.pkmDetail = pkm.data;
				})
				.catch((error) => console.log(error));

		}
	}
};
</script>
