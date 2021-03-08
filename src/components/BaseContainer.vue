<template>
    <div class="container">
        <slot></slot>
    </div>
</template>

<style lang="scss" scoped>
.container {
    margin: 0 calcRem(30px);
    max-width: 708px;

    @include tablet {
        margin: 0 auto;
    }
}
</style>