<template>
	<q-page class="column items-center">
		<q-card
			class="q-ma-sm row justify-center items-center"
			bordered
			style="min-width: 260px; max-width: 755px"
		>
			<q-toolbar class="text-secondary text-center">
				<q-toolbar-title> Choose a number or get a random one! </q-toolbar-title>
			</q-toolbar>
			<q-card-section>
				<q-input
					clearable
					clear-icon="close"
					type="number"
					color="secondary"
					v-model.number="pkmNmb"
					label="Type a number"
					:rules="[
						(val) =>
							(val > 0 && val < 906) || 'Choose a number between 1 and 905',
					]"
				>
				</q-input>
			</q-card-section>
			<q-card-section>
				<q-btn color="primary" flat icon="shuffle" label="Random" @click="clickRdm" />
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
					v-for="(items, index) in pkmDetail.objSprites"
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
				<div v-show="expanded" class="row items-start justify-around">
					<q-separator />
					<q-card class="q-ma-md my-card" flat bordered style="max-width: 220px">
						<q-toolbar class="bg-secondary text-white text-bold text-capitalize justify-center" >
							Types
						</q-toolbar>
						<q-scroll-area style="width: 210px; height: 150px;" visible>
							<q-card-section class="row justify-center" >
								<q-chip class="text-capitalize" color="accent" v-for="(item, index) in pkmDetail.types" :key="index">{{ pkmDetail.types[index].type.name.replace("-"," ")  }}</q-chip>
							</q-card-section>
						</q-scroll-area>
					</q-card>
					<q-card class="q-ma-md my-card" flat bordered style="max-width: 220px">
						<q-toolbar class="bg-secondary text-white text-bold text-capitalize justify-center" >
							Abilities
						</q-toolbar>
						<q-scroll-area style="width: 210px; height: 150px;" visible>
							<q-card-section class="row justify-center" >
								<q-chip class="text-capitalize" color="accent" v-for="(item, index) in pkmDetail.abilities" :key="index">{{  pkmDetail.abilities[index].ability.name.replace("-"," ")  }}</q-chip>
							</q-card-section>
						</q-scroll-area>
					</q-card>
					<q-card v-if="showForms" class="q-ma-md my-card" flat bordered style="max-width: 220px">
						<q-toolbar class="bg-secondary text-white text-bold text-capitalize justify-center" >
							Forms
						</q-toolbar>
						<q-scroll-area style="width: 210px; height: 150px;" visible>
							<q-card-section class="row justify-center" >
								<q-chip 
								class="text-capitalize" 
								color="accent" 
								v-for="(item, index) in pkmDetail.forms" 
								:key="index">
								{{  this.pkmDetail.forms[index].name.replace(this.pkmDetail.name,"").replace("-","")  }}
								</q-chip>
							</q-card-section>
						</q-scroll-area>
					</q-card>
					<q-card v-if="showIndices" class="q-ma-md my-card" flat bordered style="max-width: 220px">
						<q-toolbar class="bg-secondary text-white text-bold text-capitalize justify-center" >
							Game Indices
						</q-toolbar>
						<q-scroll-area style="width: 210px; height: 150px;" visible>
							<q-card-section class="row justify-center" >
								<q-chip class="text-capitalize" color="accent" v-for="(item, index) in pkmDetail.game_indices" :key="index">{{  pkmDetail.game_indices[index].version.name.replace("-"," ")  }}</q-chip>
							</q-card-section>
						</q-scroll-area>
					</q-card>
					<q-card v-if="showMoves" class="q-ma-md my-card" flat bordered style="max-width: 220px">
						<q-toolbar class="bg-secondary text-white text-bold text-capitalize justify-center" >
							Moves
						</q-toolbar>
						<q-scroll-area style="width: 210px; height: 150px;" visible>
							<q-card-section  class="row justify-center" >
								<q-chip class="text-capitalize" color="accent" v-for="(item, index) in pkmDetail.moves" :key="index">{{ pkmDetail.moves[index].move.name.replace("-"," ")  }}</q-chip>
							</q-card-section>							
						</q-scroll-area>
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
			showIndices: true,
			showForms: false,
			showMoves: false,
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
					this.pkmNmb = this.pkmDetail.id
					console.log(this.pkmDetail.id)

					if(Object.keys(this.pkmDetail.game_indices).length > 0) {
						this.showIndices = true;
					} else {
						this.showIndices = false;
					}
					if(Object.keys(this.pkmDetail.forms).length > 1) {
						this.showForms = true;
					} else {
						this.showForms = false;
					}
					if(Object.keys(this.pkmDetail.moves).length > 0) {
						this.showMoves = true;
					} else {
						this.showMoves = false;
					}
				})
				.catch((error) => console.log(error));
		},
		random() {
			return this.rdmNmb = Math.floor(Math.random() * (905 - 1) + 1);			
		},
		clickRdm() {
			this.getPkmDetail(this.basePkmDetailURL + this.random())
		}
	},
	created() {
		this.clickRdm();
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
