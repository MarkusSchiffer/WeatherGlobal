<template>
  <div v-if="all" class="container mt-5">
    <div v-for="(list, index) in allCities" :key="index" class="card text-secondary">
      <div v-b-toggle="getRegion(index)" class="card-header text-center">
        <img :src="getImage(index)" :alt="getRegion(index)" class="globe-image">
        <h3 class="display-1">
          {{ getRegion(index) }}
        </h3>
      </div>
      <b-collapse :id="getRegion(index)">
        <div v-for="city in list" :key="city.woeid" class="card-body">
          <City :name="city.name" :woeid="city.woeid" :simple="true" />
        </div>
      </b-collapse>
    </div>
  </div>
  <div v-else class="row p-2">
    <div v-for="city in fewCities" :key="city.woeid">
      <City :name="city.name" :woeid="city.woeid" :simple="false" />
    </div>
  </div>
</template>

<script>
// import axios from 'axios'
import City from '../components/City.vue'

export default {
  name: 'CityGrid',
  components: {
    City
  },
  props: {
    all: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      loading: true,
      citys: null,
      errored: false,
      allCities: [
        [
          { name: 'seattle', woeid: 2490383 },
          { name: 'los-angeles', woeid: 2442047 },
          { name: 'new-york', woeid: 2459115 },
          { name: 'rio-de-janeiro', woeid: 455825 },
          { name: 'toronto', woeid: 4118 }
        ],
        [
          { name: 'beijing', woeid: 2151330 },
          { name: 'tokyo', woeid: 1118370 },
          { name: 'shanghai', woeid: 2151849 },
          { name: 'singapore', woeid: 1062617 },
          { name: 'bangkok', woeid: 1225448 }
        ],
        [
          { name: 'saint-petersburg', woeid: 2123260 },
          { name: 'london', woeid: 44418 },
          { name: 'paris', woeid: 615702 },
          { name: 'berlin', woeid: 638242 },
          { name: 'barcelona', woeid: 753692 }
        ],
        [
          { name: 'dubai', woeid: 1940345 },
          { name: 'melbourne', woeid: 1103816 },
          { name: 'johannesburg', woeid: 1582504 },
          { name: 'cairo', woeid: 1521894 },
          { name: 'istanbul', woeid: 2344116 }
        ]
      ],
      fewCities: [
        { name: 'seattle', woeid: 2490383 },
        { name: 'new-york', woeid: 2459115 },
        { name: 'tokyo', woeid: 1118370 },
        { name: 'london', woeid: 44418 },
        { name: 'dubai', woeid: 1940345 }
      ]
    }
  },
  methods: {
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
