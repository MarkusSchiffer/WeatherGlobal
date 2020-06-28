<template>
  <div class="container">
    <h2 class="text-center display-3 text-secondary">
      Welcome to WeatherGlobal!
    </h2>
    <img src="../static/cloud.svg" class="w-35 mx-auto d-block">
    <h3>
      <nuxt-link to="/cities" class="display-4 text-center text-secondary">
        Catch a Glipse of Weather Around the World:
      </nuxt-link>
    </h3>
    <city-grid :all="false" />
    <h3 class="mt-5">
      <nuxt-link to="/blog" class="display-4 text-center text-secondary">
        Latest Thoughts on the Weather...
      </nuxt-link>
    </h3>
    <display-blog :unlimited="false" />
  </div>
</template>

<script>
import CityGrid from '../components/CityGrid.vue'
import DisplayBlog from '../components/DisplayBlog.vue'

export default {
  components: {
    CityGrid,
    DisplayBlog
  }
}
</script>

<style scoped>
.w-35 {
  width: 35%;
}
</style>
