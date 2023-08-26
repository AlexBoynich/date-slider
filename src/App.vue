<template>
  <v-app>
    <v-main>
      <input type="date" v-model="minDate">
      <input type="date" v-model="maxDate">
      <DateSlider
      :minDate="minDate"
      :maxDate="maxDate"
      />
    </v-main>
  </v-app>
</template>

<script>
import DateSlider from '@/components/DateSlider/DateSlider.vue'

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
  },

  data: () => ({
    //
  }),
};
</script>
