<template>
	<q-page class="column items-center">
		<q-card
			class="q-ma-sm column items-center"
			bordered
			style="min-width: 260px"
		>
			<q-card-section>
				<q-toolbar class="text-secondary text-center">
					<q-toolbar-title> Find your Pokémon! </q-toolbar-title>
				</q-toolbar>
				<q-input
					clearable
					clear-icon="close"
					type="number"
					color="secondary"
					v-model="pkmNmb"
					label="Type a pokémon number"
					:rules="[
						(val) =>
							(val > 0 && val < 906) || 'Please type a real pokémon',
					]"
				>
				</q-input>
			</q-card-section>
		</q-card>

		<q-card
			class="q-ma-sm column items-center"
			bordered
			style="min-width: 260px; max-width: 755px"
		>
			<q-toolbar class="bg-secondary text-white text-center text-capitalize">
				<q-toolbar-title>
					# {{ pkmDetail.id }} {{ pkmDetail.name }}
					<q-badge
						align="middle"
						v-for="(types, index) in pkmDetail.types"
						:key="index"
						class="q-ma-xs q-pa-xs bg-white text-primary text-center"
						>{{ pkmDetail.types[index].type.name }}</q-badge
					>
				</q-toolbar-title>
			</q-toolbar>
			<q-card-section class="row items-center">
				<q-list
					v-for="(sprites, index) in pkmDetail.objSprites"
					:key="index"
				>
					<q-item
						class="column items-center"
						v-if="
							pkmDetail.objSprites[index][0] == 'front_default' &&
							pkmDetail.objSprites[index][1] != null
						"
					>
						<img
							:src="pkmDetail.objSprites[index][1]"
							alt="Default"
						/>
						<q-item-label
							class="text-primary text-center text-bold text-capitalize"
							>{{
								pkmDetail.objSprites[index][0]
									.replace("front_", "")
									.replace("_", " ")
							}}</q-item-label
						>
					</q-item>
					<q-item
						class="column items-center"
						v-if="
							pkmDetail.objSprites[index][0] == 'front_female' &&
							pkmDetail.objSprites[index][1] != null
						"
					>
						<img
							:src="pkmDetail.objSprites[index][1]"
							alt="Default"
						/>
						<q-item-label
							class="text-primary text-center text-bold text-capitalize"
							>{{
								pkmDetail.objSprites[index][0]
									.replace("front_", "")
									.replace("_", " ")
							}}</q-item-label
						>
					</q-item>
					<q-item
						class="column items-center"
						v-if="
							pkmDetail.objSprites[index][0] == 'front_shiny' &&
							pkmDetail.objSprites[index][1] != null
						"
					>
						<img
							:src="pkmDetail.objSprites[index][1]"
							alt="Default"
						/>
						<q-item-label
							class="text-primary text-center text-bold text-capitalize"
							>{{
								pkmDetail.objSprites[index][0]
									.replace("front_", "")
									.replace("_", " ")
							}}</q-item-label
						>
					</q-item>
					<q-item
						class="column items-center"
						v-if="
							pkmDetail.objSprites[index][0] == 'front_shiny_female' &&
							pkmDetail.objSprites[index][1] != null
						"
					>
						<img
							:src="pkmDetail.objSprites[index][1]"
							alt="Default"
						/>
						<q-item-label
							class="text-primary text-center text-bold text-capitalize"
							>{{
								pkmDetail.objSprites[index][0]
									.replace("front_", "")
									.replace("_", " ")
							}}</q-item-label
						>
					</q-item>
				</q-list>
			</q-card-section>
			<q-card-section>
				<template class="flex flex-center">
					<q-card
						class=""
						style="width: 80px"
						flat
						bordered
					>
						<q-toolbar
							class="bg-accent text-dark text-bold justify-center"
							>Height</q-toolbar
						>
						<q-card-section class="text-center"
							>{{ pkmDetail.height }}m</q-card-section
						>
					</q-card>
					<q-card
						style="width: 80px"
						flat
						bordered
					>
						<q-toolbar
							class="bg-accent text-dark text-bold justify-center"
							>Weight</q-toolbar
						>
						<q-card-section class="text-center"
							>{{ pkmDetail.weight }}kg</q-card-section
						>
					</q-card>
					<q-card
						style="width: 80px"
						flat
						bordered
						v-for="(stat, index) in pkmDetail.stats"
						:key="index"
					>
						<q-toolbar
							class="bg-accent text-dark text-bold text-capitalize justify-center"
							>{{
								pkmDetail.stats[index].stat.name.replace("-", " ")
							}}</q-toolbar>
						<q-card-section class="text-center">{{
							pkmDetail.stats[index].base_stat
						}}</q-card-section>
					</q-card>
					<q-card
						style="width: 80px; height: 105px"
						flat
						bordered
					>
						<q-toolbar
							class="bg-accent text-dark text-bold text-capitalize justify-center"
							>More</q-toolbar
						>
						<q-card-section class="text-center">
							<q-btn
								color="grey"
								round
								flat
								dense
								:icon="
									expanded
										? 'keyboard_arrow_up'
										: 'keyboard_arrow_down'
								"
								@click="expanded = !expanded"
							/>
						</q-card-section>
					</q-card>
				</template>
			</q-card-section>
			<q-slide-transition>
				<div v-show="expanded">
					<q-separator />
					<q-card class="q-ma-md my-card" flat bordered style="max-width: 220px">
						<q-toolbar class="bg-secondary text-white text-bold text-capitalize justify-center" >
							Abilities
						</q-toolbar>
						<q-card-section class="flex flex-center" >
							<q-chip class="text-capitalize" color="accent" v-for="(item, index) in pkmDetail.abilities" :key="index">{{  pkmDetail.abilities[index].ability.name.replace("-"," ")  }}</q-chip>
						</q-card-section>
					</q-card>
					<q-card class="q-ma-md my-card" flat bordered style="max-width: 220px">
						<q-toolbar class="bg-secondary text-white text-bold text-capitalize justify-center" >
							Game Indices
						</q-toolbar>
						<q-card-section  class="flex flex-center" >
							<q-chip class="text-capitalize" color="accent" v-for="(item, index) in pkmDetail.game_indices" :key="index">{{  pkmDetail.game_indices[index].version.name.replace("-"," ")  }}</q-chip>
						</q-card-section>
					</q-card>
				</div>
			</q-slide-transition>
		</q-card>
	</q-page>
</template>

<style></style>

<script>
import axios from "axios";

export default {
	name: "PkmDetail",
	data() {
		return {
			expanded: false,
			pkmNmb: "",
			pkmDetail: {
				sprites: {},
				objSprites: {},
			},
			basePkmDetailURL: "https://pokeapi.co/api/v2/pokemon/",
		};
	},
	methods: {
		getPkmDetail(PkmDetailURL) {
			axios
				.get(PkmDetailURL)
				.then((pkm) => {
					this.pkmDetail = pkm.data;
					this.pkmDetail.weight /= 10;
					this.pkmDetail.height /= 10;
					this.pkmDetail.objSprites = Object.entries(this.pkmDetail.sprites);

					// Início rascunho


					
					console.log(this.pkmDetail);
					for (var i in this.pkmDetail.abilities) {
						console.log(this.pkmDetail.abilities[i].ability.name.replace("-"," "))
					}



					// Fim rascunho
				})
				.catch((error) => console.log(error));
		},
	},
	created() {
		this.rdmNmb = Math.floor(Math.random() * (905 - 1) + 1);
		let rdmUrl = this.basePkmDetailURL + this.rdmNmb;
		this.getPkmDetail(rdmUrl);
	},
	watch: {
		pkmNmb(NewValue) {
			const addPkmDetailURL = this.basePkmDetailURL + NewValue;
			this.getPkmDetail(addPkmDetailURL);
		},
	},
};
</script>

<style scoped>
.tagtype {
	background-color: black;
}
</style>
