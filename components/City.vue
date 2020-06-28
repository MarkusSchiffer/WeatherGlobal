<template>
  <div class="card" @click="toggleShow()">
    <img :src="image" :alt="name" class="img-fluid">
    <h4 class="text-center">
      {{ displayName(name) }}
    </h4>
    <div v-if="show">
      <div v-for="day in weather" :key="day.id" class="day m-2 border border-primary rounded">
        <img :src="getWeatherIconString(day.weather_state_abbr)" :alt="day.weather_state_name">
        <span>
          <h5>{{ getDayOfWeek(day.applicable_date) }}</h5>
          <p>{{ day.weather_state_name }}</p>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'City',
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
    },
    simple: {
      // Which type of display to use, either simple cards or accordian.
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      loadingImage: true,
      image: null,
      loadingWeather: true,
      weather: null,
      errored: false,
      show: false
    }
  },
  mounted () {
    const pathImage = 'https://api.teleport.org/api/urban_areas/slug:' + this.name + '/images/'
    const pathForecast = 'https://cors-anywhere.herokuapp.com/https://www.metaweather.com/api/location/' + this.woeid
    axios
      .get(pathImage)
      .then(response => (this.image = response.data.photos[0].image.web))
      .catch((error) => {
        this.errored = true
        return Promise.reject(error)
      })
      .finally(() => (this.loadingImage = false))
    axios
      .get(pathForecast)
      .then(response => (this.weather = response.data.consolidated_weather))
      .catch((error) => {
        this.errored = true
        return Promise.reject(error)
      })
      .finally(() => (this.loadingWeather = false))
  },
  methods: {
    // This was helpful: https://www.w3resource.com/javascript-exercises/javascript-string-exercise-9.php
    displayName (name) {
      const retVal = name.replace(/-/g, ' ')
      return retVal.replace(/\w\S*/g, function (txt) {
        return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase()
      })
    },
    // Thanks to Samuel Liew https://stackoverflow.com/questions/17964170/get-the-weekday-from-a-date-object-or-date-string-using-javascript
    getDayOfWeek (date) {
      const dayOfWeek = new Date(date).getDay()
      return isNaN(dayOfWeek) ? null : ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'][dayOfWeek]
    },
    getWeatherIconString (abbreviation) {
      return require('../assets/weathericons/' + abbreviation + '.svg')
    },
    toggleShow () {
      this.show = !this.show
    }
  }
}
</script>

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
