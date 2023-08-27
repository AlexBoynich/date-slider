<template>
  <v-app>
    <v-main>
      <!-- <input type="date" v-model="minDate">
      <input type="date" v-model="maxDate">
      <DateSlider
      :minDate="minDate"
      :maxDate="maxDate"
      /> -->
      <CustomRangeSlider/>
    </v-main>
  </v-app>
</template>

<script>
import DateSlider from '@/components/DateSlider/DateSlider.vue'
import CustomRangeSlider from './components/DateSlider/CustomRangeSlider.vue';

export default {
  name: 'App',

  data () {
    return {
      minDate: '',
      maxDate: ''
    }
  },

  components: {
    DateSlider,
    CustomRangeSlider,
  },

  data: () => ({
    //
  }),
};
</script>
