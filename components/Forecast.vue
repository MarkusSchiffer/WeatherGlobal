<!-- © Markus Schiffer, June 2020 -->
<!-- This component displays a few days worth of weather forecast. It is intended to be a child of the City component.
     This component exists so that the forecast is only fetched when needed. This way cities can be loaded independently of their forecasts. -->

<template>
  <!-- The API definatley takes its time. It's important that the user knows that this is happening and doesn't start a clicking frenzy. -->
  <div v-if="loadingWeather">
    <p>Loading...</p>
  </div>
  <!-- Regular case, there was no error loading the forecast and we can display it. -->
  <div v-else-if="!errored">
    <div v-for="day in weather" :key="day.id" class="day m-2 border border-primary rounded">
      <img :src="getWeatherIconString(day.weather_state_abbr)" :alt="day.weather_state_name">
      <span>
        <h5>{{ getDayOfWeek(day.applicable_date) }}</h5>
        <p>{{ day.weather_state_name }}</p>
      </span>
    </div>
  </div>
  <!-- This error is not too uncommon. If the API is having issues, we'll let the user know :(. -->
  <div v-else>
    <p>Sorry, it appears the API is having an issue right now {{ errorMessage }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: {
    // A citys location, needed for the API.
    woeid: {
      type: Number,
      required: true
    },
    // If we previously got the forecast data, we can just use the cached data.
    // Note, this can be null if no cached data exists.
    cached: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      loadingWeather: true, // True if the forecast is being loaded.
      weather: null, // The forecast used is stored here.
      errored: false, // True if there was an error reading the forecast.
      errorMessage: '' // If there was an error, display it with this variable.
    }
  },
  mounted () {
    // If we have cached data, use that.
    if (this.cached !== null) {
      this.weather = this.cached
      this.loadingWeather = false
      return
    }
    // No cached data. Lets get it from the API.
    const pathForecast = 'https://cors-anywhere.herokuapp.com/https://www.metaweather.com/api/location/' + this.woeid
    axios
      .get(pathForecast)
      .then((response) => {
        this.weather = response.data.consolidated_weather
        // Update the cache so we don't have to do this again.
        this.$emit('cache', this.weather)
      })
      .catch((error) => {
        this.errored = true
        this.errorMessage = error
      })
      .finally(() => (this.loadingWeather = false))
  },
  methods: {
    // Turn an ISO date (returned by the API) to a weekday (this is what users care about).
    // Thanks to Samuel Liew https://stackoverflow.com/questions/17964170/get-the-weekday-from-a-date-object-or-date-string-using-javascript
    getDayOfWeek (date) {
      const dayOfWeek = new Date(date).getDay()
      return isNaN(dayOfWeek) ? null : ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'][dayOfWeek]
    },
    // Get the correct src for the icon based on the abbreviation returned by the API.
    getWeatherIconString (abbreviation) {
      return require('../assets/weathericons/' + abbreviation + '.svg')
    }
  }
}
</script>

<!-- Style to format the forecasts' days. -->
<style scoped>
.day {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: flex-start;
  align-content: center;
}
.day > img {
  width: 50%;
  max-height: 5rem;
}
.day > span {
  display: flex;
  flex-direction: column;}
</style>
