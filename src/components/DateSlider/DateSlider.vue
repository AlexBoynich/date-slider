<template>
    <v-row>
      <v-col
      cols="auto"
      >
        <h4>Года</h4>
        <h4>Года</h4>
      </v-col>
      <v-col cols="true" class="pa-12">
        <v-range-slider
          :tick-labels="seasons"
          :value="[0, 1]"
          min="0"
          :max="seasons.length-1"
          ticks="false"
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
      </v-col>
    </v-row>
  </template>

<script>
import styles from './styles.sass'
export default {
    data: () => ({
        seasons: [
        '2014',
        '2015',
        '2016',
        '2017',
        '2018',
        '2019',
        '2020',
        '2021',
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
        ],
        icons: [
        'mdi-snowflake',
        'mdi-leaf',
        'mdi-fire',
        'mdi-water',
        ],
    }),

    methods: {
        season (val) {
        return this.icons[val]
        },
    },
    props: ['minDate', 'maxDate'],
}
</script>

<style scoped lang="sass">
.v-slider--horizontal .v-slider__track-container
    height: 10px
.v-slider__tick
  width: 0 !important
</style>