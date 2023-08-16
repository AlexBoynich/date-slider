<template>
    <div class="range-slider">
        <input type="range" min="0" max="100" step="5" v-model.number="minPrice">
        <input type="range" min="0" max="100" step="5" v-model.number="maxPrice">
    </div>
</template>

<script>
export default {
    data() {
        return {
            minPrice: 15,
            maxPrice: 30,
        }
    }
}
</script>

<style scoped lang="sass">
.range-slider
    width: 200px
    margin: auto 16px
    text-align: center
    position: relative
.range-slider input[type=range]
    position: absolute
    left: 0
input[type=range]::webkit-slider-thumb
    z-index: 2
    position: relative
    top: 2px
    margin-top: -7px
</style>