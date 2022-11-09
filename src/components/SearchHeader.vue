<template>
    <q-card>
        <q-card-section>
            <q-toolbar class="text-accent text-center">
				<q-toolbar-title>
					Qual é o Pokémon?
				</q-toolbar-title>
			</q-toolbar>
            <q-input 
                clearable 
                clear-icon="close" 
                filled 
                color="accent" 
                v-model="text" 
                label="Digite aqui o número" />
            <!-- <q-select filled v-model="model" :options=options style="width:400px"/> -->
        </q-card-section>
    </q-card>
</template>

<script>
export default {
    name: "SearchHeader",
    data() {
        return {
            options: {},
        };
    },
};
</script>
