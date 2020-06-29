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

<style>
.w-35 {
  width: 35%;
}
.display-2 {
  font-size: 3rem;
}
.display-3 {
  font-size: 2.5rem;
}
.display-4 {
  font-size: 1.5rem;
}
.display-5 {
  font-size: 1.25rem;
  font-weight: 200;
}
.lead {
  font-size: 1rem;
}
@media (min-width: 728px) {
  .display-2 {
    font-size: 4.5rem;
  }
  .display-3 {
    font-size: 4rem
  }
  .display-4 {
    font-size: 3.50rem;
  }
  .display-5 {
    font-size: 2.25rem;
  }
  .lead {
    font-size: 1.25rem;
  }
}
</style>
