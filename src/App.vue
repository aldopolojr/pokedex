<template>
    <the-header :data="data" :pokeId="pokemon.id"></the-header>
    <the-list v-if="data.startPage"></the-list>
    <the-overview v-else :pokemon="pokemon"></the-overview>
    <the-modal v-show="data.modalOpen"></the-modal>
</template>

<script>
import TheHeader from './components/TheHeader.vue';
import TheList from './components/TheList.vue';
import TheOverview from './components/TheOverview.vue';
import TheModal from './components/TheModal.vue';

export default {
    components: { TheHeader, TheList, TheOverview, TheModal },
    data() {
        return {
            data: {
                startPage: true,
                title: 'pokédex',
                modalOpen: false,
            },
            pokemon: {
                id: null,
                name: null,
                img: null,
                types: null,
                height: null,
                weight: null,
                abilities: null,
                moves: null,
                stats: null,

            },
        };
    },
    provide() {
        return {
            data: this.data,
            openList: this.openList,
            loadPokemon: this.loadPokemon,
            toggleModal: this.toggleModal,
        };
    },
    methods: {
        loadPokemon(pokemon) {
            fetch(`https://pokeapi.co/api/v2/pokemon/${pokemon}`)
            .then(response => {
                if (response.ok) {
                    return response.json();
                } else {
                    // throw error
                }
            })
            .then(data => { 
                this.pokemon.id = data.id;
                this.pokemon.name = data.name;
                this.pokemon.img = data.sprites.front_default;
                this.pokemon.types = data.types.map(x => x.type.name);
                this.pokemon.height = data.height;
                this.pokemon.weight = data.weight;
                this.pokemon.abilities = data.abilities.map(x => x.ability.name);
                this.pokemon.moves = data.moves.map(x => x.move.name);
                this.pokemon.stats = data.stats.map(x => x.base_stat);

                this.data.startPage = false;
                this.data.title = data.name;
                window.scrollTo(0, 0);
            })
            .catch(error => { console.log(error); });
        },
        openList() {
            this.data.startPage = true;
            this.data.title = 'pokédex';
        },
        toggleModal() {
            this.data.modalOpen = !this.data.modalOpen;
        },
    }
}
</script>

<style lang="scss">
@import "@/assets/sass/typography.scss";
@import "@/assets/sass/reset.scss";

</style>