<!-- © Markus Schiffer, June 2020 -->
<!-- This is the only layout needed for the whole site. Ensures the header is present,
     and sets style rules for display-2 -->

<template>
  <div>
    <CGHeader />
    <nuxt />
  </div>
</template>

<script>
import CGHeader from '~/components/Header.vue'

export default {
  name: 'DefaultLayout',
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
