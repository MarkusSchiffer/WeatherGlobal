<!-- © Markus Schiffer, June 2020 -->
<!-- This component displays multiple cities. It is used (albeit differently) on both the home and cities pages. -->

<template>
  <!-- The default case, the parent wants all of the cities to be displayed. -->
  <div v-if="all" class="container mt-5">
    <!-- The card that expands, holds all the cities in a region. -->
    <div v-for="(list, index) in allCities" :key="index" class="card text-secondary">
      <div v-b-toggle="getRegion(index)" class="card-header text-center">
        <img :src="getImage(index)" :alt="getRegion(index)" class="globe-image">
        <h3 class="display-1">
          {{ getRegion(index) }}
        </h3>
      </div>
      <!-- The collapsible element which stores all cites in a given region. -->
      <b-collapse :id="getRegion(index)">
        <div v-for="city in list" :key="city.woeid" class="card-body">
          <City :name="city.name" :woeid="city.woeid" />
        </div>
      </b-collapse>
    </div>
  </div>
  <!-- The case where the parent just wants to see a few cities. -->
  <div v-else class="row p-2">
    <div v-for="city in fewCities" :key="city.woeid">
      <City :name="city.name" :woeid="city.woeid" />
    </div>
  </div>
</template>

<script>
import City from '../components/City.vue'
import json from '../assets/cities.json'

export default {
  name: 'CityGrid',
  components: {
    City
  },
  props: {
    // Whether to display all cities or just some. Defaults to all.
    all: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      allCities: json.allCities, // We need to read in the list of all cities.
      fewCities: json.fewCities // We need just a few cities.
    }
  },
  methods: {
    // Figures out the region of cities based on the list they are in.
    getRegion (index) {
      if (!this.all) {
        return 'Top Global'
      }
      switch (index) {
        case 0:
          return 'Americas'
        case 1:
          return 'Asia'
        case 2:
          return 'Europe'
        case 3:
          return 'Other'
      }
    },
    getImage (index) {
      // Gets the correct global image based on list of images used.
      if (!this.all) {
        return null
      }
      switch (index) {
        case 0:
          return require('../static/Americas.svg')
        case 1:
          return require('../static/Asia.svg')
        case 2:
          return require('../static/Europe.svg')
        case 3:
          return require('../static/Globe.svg')
      }
    }
  }
}
</script>

<!-- All styling makes sure the accordions display nicely on all screen sizes. -->
<style scoped>
.globe-image {
  max-height: 7rem;
}
.card-header {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.card-header > img {
  margin-left: 2rem;
  margin-right: 4rem;
}
.display-1 {
  font-size: 3rem;
}

@media (min-width: 768px) {
  .display-1 {
    font-size: 4.5rem;
  }
  .card-header > img {
    margin-left: 5rem;
    margin-right: 7rem;
  }
  .globe-image {
    max-height: 10rem;
  }
}
@media (min-width: 992px) {
  .display-1 {
    font-size: 6rem;
  }
  .globe-image {
    max-height: 15rem;
  }
  .card-header > img {
    margin-left: 8rem;
    margin-right: 10rem;
  }
}
</style>
