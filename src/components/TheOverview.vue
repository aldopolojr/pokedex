<template>
    <div class="overview">
        <section class="overview__sprite">
            <base-container>
                <div class="content">
                    <img :src="pokemon.img" :alt="pokemon.name">
                    <p>#{{ pokemon.id }}</p>
                </div>
            </base-container>
        </section>

        <h2>{{ types }}</h2>
        <section class="overview__stats">
            <base-container>
                <div class="overview__stats-group">
                    <p>HP</p>
                    <div class="stat-bar"><span :style="`width: ${pokemon.stats[0]}%;`"></span></div>
                </div>
                <div class="overview__stats-group">
                    <p>Attack</p>
                    <div class="stat-bar"><span :style="`width: ${pokemon.stats[1]}%;`"></span></div>
                </div>
                <div class="overview__stats-group">
                    <p>Defense</p>
                    <div class="stat-bar"><span :style="`width: ${pokemon.stats[2]}%;`"></span></div>
                </div>
                <div class="overview__stats-group">
                    <p>SP Attack</p>
                    <div class="stat-bar"><span :style="`width: ${pokemon.stats[3]}%;`"></span></div>
                </div>
                <div class="overview__stats-group">
                    <p>SP Defense</p>
                    <div class="stat-bar"><span :style="`width: ${pokemon.stats[4]}%;`"></span></div>
                </div>
                <div class="overview__stats-group">
                    <p>Speed</p>
                    <div class="stat-bar"><span :style="`width: ${pokemon.stats[5]}%;`"></span></div>
                </div>
            </base-container>
        </section>

        <h2>Profile</h2>
        <section class="overview__profile">
            <base-container>
                <div class="overview__profile-group">
                    <p class="key">Height</p>
                    <p class="val">{{ height }}</p>
                </div>
                <div class="overview__profile-group">
                    <p class="key">weight</p>
                    <p class="val">{{ weight }}</p>
                </div>
                <div class="overview__profile-group">
                    <p class="key">Abilities</p>
                    <p class="val">{{ abilities }}</p>
                </div>
            </base-container>
        </section>

        <h2>Moves</h2>
        <section class="overview__moves">
            <base-container>
                <ul>
                    <li v-for="move in pokemon.moves" :key="move">{{ move }}</li>
                </ul>
            </base-container>
        </section>
    </div>
</template>

<script>
export default {
    props: ['pokemon'],
    computed: {
        types() {
            return this.pokemon.types.join(" / ");
        },
        height() {
            return this.pokemon.height / 10 + " m";
        },
        weight() {
            return this.pokemon.weight / 10 + " kg";
        },
        abilities() {
            return this.pokemon.abilities.join(", ");
        },
    },
}
</script>

<style lang="scss" scoped>
.overview {
    section {
        padding: calcRem(20px) 0;
    }

    h2 {
        padding: calcRem(10px) 0;
        background: $red-light;
        color: $white;
        font-size: calcRem(12px);
        font-weight: 400;
        text-align: center;
        text-transform: uppercase;
    }
}

section.overview__sprite {
    padding: 0;
    background: $grey;

    .content {
        position: relative;
        padding: calcRem(25px) 0;
        text-align: center;
    }

    p {
        position: absolute;
        right: calcRem(15px);
        bottom: calcRem(10px);
        color: $black;
    }
}

.overview__stats-group {
    display: flex;
    align-items: center;
    margin-bottom: calcRem(10px);

    &:last-child {
        margin-bottom: 0;
    }

    p {
        width: 100px;
        color: $black;
    }

    .stat-bar {
        flex: auto;
        position: relative;
        height: 10px;
        background: $grey;
    }

    span {
        position: absolute;
        top: 0;
        left: 0;
        display: inline-block;
        max-width: 100%;
        height: 10px;
        background: $red-light;
    }
}

.overview__profile-group {
    display: flex;
    align-items: center;
    margin-bottom: calcRem(10px);

    &:last-child {
        margin-bottom: 0;
    }

    .key {
        width: 100px;
        color: $black;
    }

    .val {
        flex: auto;
        color: $red-light;
    }
}

.overview__moves {
    ul {
        display: flex;
        flex-wrap: wrap;
        list-style: square;
        list-style-position: inside;
        color: $red-light;
    }

    li {
        width: 100%;

        @include phone-md {
            width: 50%;
        }
    }
}
</style>