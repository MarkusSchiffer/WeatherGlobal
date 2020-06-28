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
  components: {
    CityGrid
  }
}
</script>
