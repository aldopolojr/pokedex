<template>
    <header class="header">
        <base-container>
            <div class="header__content">
                <div class="header__group">
                    <a v-show="!data.startPage" @click="openList"><i class="icon icon-apps"></i></a>
                </div>
                <div class="header__group">
                    <a v-show="!data.startPage" @click="previous(pokeId)"><i class="icon icon-arrow-left"></i></a>
                    <h1>{{ data.title }}</h1>
                    <a v-show="!data.startPage" @click="next(pokeId)"><i class="icon icon-arrow-right"></i></a>
                </div>
                <div class="header__group">
                    <a @click="toggleModal"><i class="icon icon-search"></i></a>
                </div>
            </div>
        </base-container>
    </header>
</template>

<script>
export default {
    inject: ['data', 'openList' , 'loadPokemon', 'toggleModal'],
    props: ['pokeId'],
    methods: {
        previous(i) {
            if (i == 1) {
                this.loadPokemon(386);
            } else {
                this.loadPokemon(--i);
            }
        },
        next(i) {
            if (i == 386) {
                this.loadPokemon(1);
            } else {
                this.loadPokemon(++i);
            }
        },
    },
}
</script>

<style lang="scss" scoped>
.header {
    position: sticky;
    top: 0;
    background: $red-light;
    color: $white;
    z-index: 1;

    &__content {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 60px;
    }

    &__group {
        display: flex;
        align-items: center;
    }

    h1 {
        width: 110px;
        font-size: calcRem(12px);
        font-weight: 400;
        text-align: center;
        text-transform: uppercase;
    }
}
</style>