<template>
    <v-row>
      <v-col
      cols="auto" class="checks"
      >
        <h4 class="check" :class="{active: isYearSlider}" @click="changeToYears">Все года</h4>
        <h4 class="check" :class="{active: !isYearSlider}" @click="changeToMonthes">Месяца</h4>
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
              {{ label(props.value) }}
            </v-icon>
          </template>
          <template v-slot:label="props">
            {{ label(props.value) }}
          </template>
        </v-range-slider>
        <v-range-slider
        v-if="!isYearSlider"
        :tick-labels="seasons"
        v-model="range2"
        value="distance2"
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
      date: {
        startDate: ['2014', '5'],
        endDate: ['2021', '9']
      },
      startRangeDate: 15,
      endRangeDate: 43,
      range1: [0, 1],
      range2: [0, 1],
      distance2: [0, 1],
      seasons: [],
      seasonsDistance: 2,
      fullSeasons: [],
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
      getMonthes(start, end, result) {
        for (let i = start.getFullYear(); i <= end.getFullYear(); i++) {
          result.push(i)
          if (i !== end.getFullYear()) {
            result.push(...this.monthes)
          }
        }
      },
        label (val) {
        return this.labels[val]
        },
        season (val) {
        return this.fullSeasons[val]
        },
        rotateFirstLabel() {
          document.querySelector('.v-slider__thumb-label').classList.add('start-thumb-label')
        },
        changeToYears(){
          this.isYearSlider = true
          this.rotateFirstLabel()
        },
        changeSeasons() {
          const result = []
        for (let i = this.labels[this.range1[0]].split(' ')[0]; i <= (Number(this.labels[this.range1[0]].split(' ')[0]) + 2); i++) {
          result.push(i)
          this.fullSeasons.push(i)
          if (i !== (Number(this.labels[this.range1[0]].split(' ')[0]) + this.seasonsDistance)) {
            result.push(...this.monthes)
          }
        }
        
        this.seasons = result.map((item, index) => {
          return (typeof(item) !=='number' && index>0) ? String(item).substr(0, 3) : item
        })
        const res = []
        let num = Number(this.labels[this.range1[0]].split(' ')[0])
        result.reduce((acc, item, index) => {
          if (typeof(item)==='number') {
            num = item
            return res.push(`${item}`)
          } else 
          return res.push(`${num} ${item}`)

        }, 0)
        return this.fullSeasons = res

      },
        changeToMonthes(){
          this.isYearSlider = false
          this.rotateFirstLabel()
          this.changeSeasons()
        },
    },
    computed: {
      yearsMassive() {
        const start = new Date(...this.date.startDate)
        const end = new Date(...this.date.endDate)
        const result = []
        this.getMonthes(start, end, result)
        return result
      },
      years() {
        return this.yearsMassive.map(item => {
          return (typeof(item) !== 'number') ? '' : item
        })
      },
      labels () {
        const start = new Date(...this.date.startDate)
        const end = new Date(...this.date.endDate)
        const result = []
        this.getMonthes(start, end, result)
        const res = []
        let num = start.getFullYear()
        result.reduce((acc, item, index) => {
          if (typeof(item)==='number') {
            num = item
            return res.push(`${item}`)
          } else 
          return res.push(`${num} ${item}`)

        }, 0)
        return res
      },
    },
    mounted() {
      this.rotateFirstLabel()
    },
}
</script>

<style scoped lang="sass">
.v-slider--horizontal .v-slider__track-container
    height: 10px
.v-slider__tick
  width: 0 !important
.start-thumb-label
  transform: rotate(180deg) !important
.checks
  padding: 100px 20px
  line-height: 2
  @media( max-width: 1000px)
    padding: 100px 0 100px 20px
.check
  color: rgba(1, 103, 179, 1)
  opacity: 0.5
  cursor: pointer 
  text-decoration-line: underline
  text-underline-offset: 4px
  text-decoration-thickness: 2px
  @media( max-width: 1000px)
    font-size: 0.5em
.active
  opacity: 1 !important
  text-decoration: none
</style>