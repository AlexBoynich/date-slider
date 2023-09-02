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
          thumb-color="white"
          track-size="10px"
          class="range-slider"
        >
          <template v-slot:thumb-label="props"
          thumb="white">
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
        thumb-color="white"
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
      startDate: new Date ('2014-05-01'),
      endDate: new Date('2021-09-01'),
      startRangeDate: 15,
      endRangeDate: 43,
      range1: [0, 1],
      range2: [0, 1],
      distance2: [0, 1],
      seasons: [],
      seasonsDistance: 2,
      fullSeasons: [],
        monthes: [
        'Февраль',
        'Март',
        'Апрель',
        'Май',
        'Июнь',
        'Июль',
        'Август',
        'Сентябрь',
        'Октябрь',
        'Ноябрь',
        'Декабрь',
        ]
    }),

    methods: {
      getMonthes(start, end, result) {
        for (let i = this.startDate.getFullYear(); i <= end.getFullYear(); i++) {
          result.push(i)
          if (i !== this.endDate.getFullYear()) {
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
        for (let i = this.labels[this.range1[0]].split(' ')[1]; i <= (Number(this.labels[this.range1[0]].split(' ')[1]) + 2); i++) {
          result.push(i)
          this.fullSeasons.push(i)
          if (i !== (Number(this.labels[this.range1[0]].split(' ')[1]) + this.seasonsDistance)) {
            result.push(...this.monthes)
          }
        }
        
        this.seasons = result.map((item, index) => {
          return (typeof(item) !=='number' && index>0) ? String(item).substr(0, 3) : item
        })
        const res = []
        console.log(this.labels[this.range1[0]].split(' ')[1])
        let num = Number(this.labels[this.range1[0]].split(' ')[1])
        result.forEach((item) => {
          if (typeof(item)==='number') {
            num = item
            return res.push(`Январь ${item}`)
          } else 
          return res.push(`${item} ${num}`)

        })
        res[0] = `Январь ${this.labels[this.range1[0]].split(' ')[1]}`
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
        const result = []
        this.getMonthes(this.startDate, this.endDate, result)
        return result
      },
      years() {
        return this.yearsMassive.map(item => {
          return (typeof(item) !== 'number') ? '' : item
        })
      },
      labels () {
        const result = []
        this.getMonthes(this.startDate, this.endDate, result)
        const res = []
        let num = this.startDate.getFullYear()
        result.forEach((item) => {
          if (typeof(item)==='number') {
            num = item
            return res.push(`Январь ${item}`)
          } else 
          return res.push(`${item} ${num}`)

        })
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