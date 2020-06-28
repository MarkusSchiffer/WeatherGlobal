<!-- © Markus Schiffer, June 2020 -->
<!-- One of the more complicated parts of the project, this component stores one individual city. -->

<template>
  <!-- This div represents the standard city picture and name always visible -->
  <div v-if="!errored" class="card" @click="toggleShow()">
    <img :src="image" :alt="name" class="img-fluid">
    <h4 class="text-center">
      {{ displayName(name) }}
    </h4>
    <!-- Shows the actual weather forecast, but only if the user toggled the city image. Attempts to use cached data to avoid repeatedly calling the API. -->
    <div v-if="show">
      <forecast :cached="cached" :woeid="woeid" @cache="handleCache" />
    </div>
  </div>
  <!-- There was an API error loading the picture. Never had this problem. -->
  <div v-else>
    <p>Sorry, but it seems the API was unable to load the picture {{ errorMessage }}</p>
  </div>
</template>

<script>
import axios from 'axios'
import Forecast from '../components/Forecast.vue'

export default {
  name: 'City',
  components: {
    Forecast
  },
  props: {
    name: {
      // The name of the city.
      type: String,
      required: true
    },
    woeid: {
      // Location of the city, used for APIs.
      type: Number,
      required: true
    }
  },
  data () {
    return {
      loadingImage: true, // True while the image is being loaded.
      image: null, // The src text of the image to be used, from the API.
      errored: false, // There was an error loading the image.
      show: false, // True if the user wishes to see the forecast of this city.
      errorMessage: '', // If there is an error message, it is saved in the variable.
      cached: null // The cached weather forcast. Since the Forecast component is dis-mounted if show is false, cacheing its value improves performance.
    }
  },
  mounted () {
    // First we fetch the picture from the API.
    const pathImage = 'https://api.teleport.org/api/urban_areas/slug:' + this.name + '/images/'
    axios
      .get(pathImage)
      .then(response => (this.image = response.data.photos[0].image.web))
      .catch((error) => {
        this.errored = true
        this.errorMessage = error
      })
      .finally(() => (this.loadingImage = false))
  },
  methods: {
    // Display the city name with proper capitalization and no '-' characters
    // This was helpful: https://www.w3resource.com/javascript-exercises/javascript-string-exercise-9.php
    displayName (name) {
      const retVal = name.replace(/-/g, ' ')
      return retVal.replace(/\w\S*/g, function (txt) {
        return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase()
      })
    },
    // Flips the show variable for the forecast, called on click.
    toggleShow () {
      this.show = !this.show
    },
    // If the Forecast component called the API, it sends its parent (this city) that fetched data.
    // This way, if the user re-shows the forecast, we do not have to call the API again, and use cached data instead.
    handleCache (data) {
      this.cached = data
    }
  }
}
</script>
