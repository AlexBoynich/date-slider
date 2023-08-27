<template>
  <v-app>
    <v-main>
      <DateSlider
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

    }
  },

  components: {
    DateSlider,
  },

};
</script>
