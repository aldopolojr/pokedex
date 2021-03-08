<template>
    <div class="overlay" @click="toggleModal">
        <div class="modal" @click.stop>
            <input type="text" placeholder="name or index" @keyup.enter="validate" ref="searchInput">
            <button @click="validate"><i class="icon icon-search"></i></button>
        </div>
    </div>
</template>

<script>
export default {
    inject: ['loadPokemon', 'toggleModal'],
    methods: {
        validate() {
            this.loadPokemon(this.$refs.searchInput.value);
            this.toggleModal();
            this.$refs.searchInput.value = '';
        },
    },
}
</script>

<style lang="scss" scoped>
.overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background: rgba($black, 0.75);
    z-index: 10;
}

.modal {
    input {
        padding: calcRem(20px);
        color: $black;
        border: none;
        border-radius: 0;
        outline: 0;
    }

    button {
        padding: calcRem(20px);
        background: $red-light;
        color: $white;
        border: none;
        border-radius: 0;
        outline: 0;
        cursor: pointer;
    }
}
</style>