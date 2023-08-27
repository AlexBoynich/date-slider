<template>
    <div class="wrapper">
        <div class="values">
            <span id="range1">
                0
            </span>
            <span> &dash; </span>
            <span id="range2">
                100
            </span>
        </div>
        <div class="container">
            <div class="slider-track"></div>
            <input type="range" min="0" max="100" value="30" id="slider-1" @input="slideOne()">
            <input type="range" min="0" max="100" value="70" id="slider-2" @input="slideTwo()">
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            minGap: 10,
            max: 0,
            min: 100,
        }
    },
    computed: {
        sliderOne: function () {
            return document.getElementById("slider-1")
        },
        sliderTwo: function () {
            return document.getElementById("slider-2")
        },
        displayValOne: function () {
            return document.getElementById("range1")
        },
        displayValTwo: function () {
            return document.getElementById("range2")
        },
        sliderTrack: function () {
            return document.querySelector(".slider-track")
        },
        sliderMaxValue: function () {
            return document.getElementById("slider-1").max
        },
    },
    methods: {
        fillColor(){
            let sliderOne = document.getElementById("slider-1")
            let sliderTwo = document.getElementById("slider-2")
            let sliderMaxValue = document.getElementById("slider-1").max
            let sliderTrack = document.querySelector(".slider-track")
            console.log(this.max, sliderMaxValue)
            let percent1 = (sliderOne.value / sliderMaxValue) * 100
            let percent2 = (sliderTwo.value / sliderMaxValue) * 100
            sliderTrack.style.background = `linear-gradient(to right, #dadae5 ${percent1}% , #3264fe ${percent1}% , #3264fe ${percent2}%, #dadae5 ${percent2}%)`
        },
        slideOne(){
            let sliderOne = document.getElementById("slider-1")
            let sliderTwo = document.getElementById("slider-2")
            let displayValOne = document.getElementById("range1")
            if(parseInt(sliderTwo.value) - parseInt(slideOne.value) <= this.minGap){
                sliderOne.value = parseInt(sliderTwo.value) - this.minGap
            }
            displayValOne.textContent = sliderOne.value
            fillColor();
        },
        slideTwo(){
            let sliderOne = document.getElementById("slider-1")
            let sliderTwo = document.getElementById("slider-2")
            let displayValTwo = document.getElementById("range2")
            if(parseInt(sliderTwo.value) - parseInt(sliderOne.value) <= this.minGap){
                sliderTwo.value = parseInt(sliderOne.value) + this.minGap
            }
            displayValTwo.textContent = sliderTwo.value
            fillColor();
        },
    },
    mounted() {
        slideOne()
        slideTwo()
    }
}

</script>

<style scoped lang="sass">
.wrapper
    position: relative
    width: 95vmin
    background-color: #ffffff
    padding: 50px 40px 20px 40px
    border-radius: 10px
.container
    position: relative
    width: 100%
    height: 100px
    margin-top: 30px
input[type="range"]
    -webkit-appearance: none
    -moz-appearance: none
    appearance: none
    width: 100%
    outline: none
    position: absolute
    margin: auto
    top: 0
    bottom: 0
    background-color: transparent
    pointer-events: none
.slider-track
    width: 100%
    height: 5px
    position: absolute
    margin: auto
    top: 0
    bottom: 0
    border-radius: 5px
    background: red
input[type="range"]::-webkit-slider-runnable-track
    -webkit-appearance: none
    height: 5px
input[type="range"]::-moz-range-track
    -moz-appearance: none
    height: 5px
input[type="range"]::-ms-track
    appearance: none
    height: 5px
input[type="range"]::-webkit-slider-thumb
    -webkit-appearance: none
    height: 1.7em
    width: 1.7em
    background-color: #3264fe
    cursor: pointer
    margin-top: -9px
    pointer-events: auto
    border-radius: 50%
input[type="range"]::-moz-range-thumb
    -webkit-appearance: none
    height: 1.7em
    width: 1.7em
    cursor: pointer
    border-radius: 50%
    background-color: #3264fe
    pointer-events: auto
input[type="range"]::-ms-thumb
    appearance: none
    height: 1.7em
    width: 1.7em
    cursor: pointer
    border-radius: 50%
    background-color: #3264fe
    pointer-events: auto
input[type="range"]:active::-webkit-slider-thumb
    background-color: #ffffff
    border: 3px solid #3264fe
.values
    background-color: #3264fe
    width: 32%
    position: relative
    margin: auto
    padding: 10px 0
    border-radius: 5px
    text-align: center
    font-weight: 500
    font-size: 25px
    color: #ffffff
.values:before
    content: ""
    position: absolute
    height: 0
    width: 0
    border-top: 15px solid #3264fe
    border-left: 15px solid transparent
    border-right: 15px solid transparent
    margin: auto
    bottom: -14px
    left: 0
    right: 0

</style>