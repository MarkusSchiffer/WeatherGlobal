<!-- © Markus Schiffer, June 2020 -->
<!-- The main cities. Loads the city grid with no restrictions. -->

<template>
  <div class="mt-5">
    <h1 class="display-2 text-center text-primary">
      {{ title }}
    </h1>
    <CityGrid />
  </div>
</template>

<script>
import CityGrid from '../components/CityGrid.vue'

export default {
  name: 'Cities',
  components: {
    CityGrid
  },
  data () {
    return {
      title: 'Choose a City to View its Weather:'
    }
  },
  head () {
    return {
      title: this.title,
      meta: [
        { hid: 'description', name: 'description', content: 'Select a city to view its weather. Cities are grouped into Americas, Asia, Europe, and other Global. Just click the pictures and explore!' }
      ]
    }
  }
}
</script>
