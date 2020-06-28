<template>
  <div>
    <CGHeader />
    <nuxt />
  </div>
</template>

<script>
import CGHeader from '~/components/Header.vue'

export default {
  components: {
    CGHeader
  }
}
</script>

<style scoped>
.display-2 {
  font-size: 3rem;
}

@media (min-width: 768px) {
  .display-2 {
    font-size: 4.5rem;
  }
}
</style>
