<!-- © Markus Schiffer, June 2020 -->
<!-- The main cities. Loads the city grid with no restrictions. -->

<template>
  <div class="mt-5">
    <h2 class="display-2 text-center text-primary">
      Choose a City:
    </h2>
    <CityGrid />
  </div>
</template>

<script>
import CityGrid from '../components/CityGrid.vue'

export default {
  name: 'Cities',
  components: {
    CityGrid
  }
}
</script>
