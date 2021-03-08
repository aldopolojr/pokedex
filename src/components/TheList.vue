<template>
    <ul class="list">
        <li v-for="pokemon in pokemonList" :key="pokemon.name">
            <base-container>
                <a @click=loadPokemon(pokemon.name)>{{ pokemon.name }}</a>
            </base-container>
        </li>
    </ul>
</template>

<script>
export default {
    inject: ['loadPokemon'],
    data() {
        return {
            pokemonList: [],
        };
    },
    beforeCreate() {
        fetch('https://pokeapi.co/api/v2/pokemon?offset=0&limit=386')
        .then(response => {
            if (response.ok) {
                return response.json();
            } else {
                // throw error
            }
        })
        .then(data => { this.pokemonList = data.results; })
        .catch(error => { console.log(error); });
    },
}
</script>

<style lang="scss" scoped>
.list {
    list-style: none;
    counter-reset: items;

    li {
        padding: calcRem(15px) 0;
        color: $red-light;
        text-transform: capitalize;
        counter-increment: items;

        &:nth-child(even) {
            background: $grey;
            color: $red-dark;
        }

        a {
            cursor: pointer;
        }
    }

    li a:before { content: "#00" counter(items)". "; }
    li:nth-child(n+10) a:before { content: "#0" counter(items)". "; }
    li:nth-child(n+100) a:before { content: "#" counter(items)". "; }
}
</style>