<template>
    <v-row>
      <v-col
      cols="auto"
      >
        <h4 @click="changeToYears">Все года</h4>
        <h4 @click="changeToMonthes">Месяца</h4>
      </v-col>
      <v-col cols="true" class="pa-12">
        <v-range-slider
          v-if="isYearSlider"
          :tick-labels="years"
          v-model="range1"
          min="0"
          :max="years.length-1"
          tick-size="4"
          thumb-label="always"
          track-color="rgba(237, 241, 248, 1)"
          track-size="10px"
          class="range-slider"
        >
          <template v-slot:thumb-label="props">
            <v-icon dark>
              {{ season(props.value) }}
            </v-icon>
          </template>
          <template v-slot:label="props">
            {{ season(props.value) }}
          </template>
        </v-range-slider>
        <v-range-slider
        v-if="!isYearSlider"
        :tick-labels="seasons"
        v-model="range2"
        value="range2"
        min="0"
        :max="seasons.length-1"
        tick-size="4"
        thumb-label="always"
        track-color="rgba(237, 241, 248, 1)"
        track-size="10px"
        class="range-slider"
      >
        <template class="endThumbLabel" v-slot:thumb-label="props">
            {{ season(props.value) }}
        </template>
        <template v-slot:label="props">
          {{ season(props.value) }}
        </template>
      </v-range-slider>
      </v-col>
    </v-row>
  </template>

<script>
import styles from './styles.sass'
export default {
    data: () => ({
      isYearSlider: true,
      startDate: ['2014', '5'],
      endDate: ['2021', '9'],
      startRangeDate: 0,
      endRangeDate: 1,
      range1: [0, 1],
      range2: [0, 1],
        seasons: [
        '2017',
        'февраль',
        'март',
        'апрель',
        'май',
        'июнь',
        'июль',
        'август',
        'сентябрь',
        'октябрь',
        'ноябрь',
        'декабрь',
        '2018',
        'февраль',
        'март',
        'апрель',
        'май',
        'июнь',
        'июль',
        'август',
        'сентябрь',
        'октябрь',
        'ноябрь',
        'декабрь',
        '2019',
        ],
        icons: [
        'mdi-snowflake',
        'mdi-leaf',
        'mdi-fire',
        'mdi-water',
        ],
        monthes: [
        'февраль',
        'март',
        'апрель',
        'май',
        'июнь',
        'июль',
        'август',
        'сентябрь',
        'октябрь',
        'ноябрь',
        'декабрь',
        ]
    }),

    methods: {
        season (val) {
        return this.labels[val]
        },
        rotateFirstLabel() {
          document.querySelector('.v-slider__thumb-label').classList.add('start-thumb-label')
        },
        changeToYears(){
          this.isYearSlider = true
          this.rotateFirstLabel()
        },
        changeToMonthes(){
          this.isYearSlider = false
          this.rotateFirstLabel()
        },
    },
    computed: {
      yearsMassive() {
        let start = new Date(...this.startDate)
        let end = new Date(...this.endDate)
        let result = []
        for (let i = start.getFullYear(); i <= end.getFullYear(); i++) {
          result.push(i)
          if (i !== end.getFullYear()) {
            result.push(...this.monthes)
          }
        }
        return result
      },
      years() {
        return this.yearsMassive.map(item => {
          if (typeof(item) !== 'number') {
            return ''
          } else 
          return item
        })
      },
      labels () {
        let start = new Date(...this.startDate)
        let end = new Date(...this.endDate)
        let result = []
        for (let i = start.getFullYear(); i <= end.getFullYear(); i++) {
          result.push(i)
          if (i !== end.getFullYear()) {
            result.push(...this.monthes)
          }
        }
        return result
      }
    },
    mounted() {
      this.rotateFirstLabel()
    }
}
</script>

<style scoped lang="sass">
.v-slider--horizontal .v-slider__track-container
    height: 10px
.v-slider__tick
  width: 0 !important
.start-thumb-label
  transform: rotate(180deg) !important
</style>