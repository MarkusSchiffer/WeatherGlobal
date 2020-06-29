<!-- © Markus Schiffer, June 2020 -->
<!-- The landing page. Shows parts of the site's two main features, the forecasts by city and the blog. -->

<template>
  <div class="container">
    <h1 class="text-center display-3 text-secondary">
      {{ title }}
    </h1>
    <img src="../static/cloud.svg" class="w-35 mx-auto d-block">
    <h2>
      <nuxt-link to="/cities" class="display-4 text-center text-secondary">
        Catch a Glipse of Weather Around the World:
      </nuxt-link>
    </h2>
    <!-- Set all to false to only select a few cities. -->
    <city-grid :all="false" />
    <h2 class="mt-3">
      <nuxt-link to="/blog" class="display-4 text-center text-secondary">
        Latest Thoughts on the Weather...
      </nuxt-link>
    </h2>
    <!-- Set unlimited to false to only show the three newest blog posts. -->
    <display-blog :unlimited="false" />
  </div>
</template>

<script>
import CityGrid from '../components/CityGrid.vue'
import DisplayBlog from '../components/DisplayBlog.vue'

export default {
  name: 'Home',
  components: {
    CityGrid,
    DisplayBlog
  },
  data () {
    return {
      title: 'Welcome to Weather-Global!' // Page title (meta).
    }
  },
  head () {
    return {
      title: this.title,
      meta: [
        { hid: 'description', name: 'description', content: "Weather-Global Home Page: Welcome! Let's see what's new!" }
      ]
    }
  }
}
</script>
