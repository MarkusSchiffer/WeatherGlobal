<!-- © Markus Schiffer, June 2020 -->
<!-- This is the site header. It uses Bootstap's special Vue.js elements for simple implementation -->

<template>
  <header class="fix-offset">
    <b-navbar toggleable="md" type="dark" variant="secondary" fixed="top">
      <nuxt-link class="navbar-brand" to="/">
        <img
          src="../static/cloud.svg"
          alt="car logo"
          width="30"
          height="30"
          class="d-inline-block align-top"
          xmlns:svg="http://www.w3.org/2000/svg"
        >
        Weather-Global
      </nuxt-link>
      <b-navbar-toggle target="nav-collapse" />
      <!-- Make collapsable for small screens. -->
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <nuxt-link class="nav-link" to="/">
            Home <span v-if="currentPage === 0" class="sr-only">(current)</span>
          </nuxt-link>
          <nuxt-link class="nav-link" to="/cities">
            Cities <span v-if="currentPage === 1" class="sr-only">(current)</span>
          </nuxt-link>
          <nuxt-link class="nav-link" to="/blog">
            Blog <span v-if="currentPage === 2" class="sr-only">(current)</span>
          </nuxt-link>
          <nuxt-link class="nav-link" to="/resources">
            Learn More <span v-if="currentPage === 3" class="sr-only">(current)</span>
          </nuxt-link>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </header>
</template>

<script>
export default {
  name: 'Header',
  computed: {
    // Helps the screen reader announce the current page.
    currentPage () {
      const path = this.$route.path
      if (path.includes('cities')) {
        return 1
      } else if (path.includes('blog')) {
        return 2
      } else if (path.includes('resources')) {
        return 3
      } else {
        return 0
      }
    }
  }
}
</script>

<!-- This style accounts for bolding/white the current nav link -->
<style scoped>
.fix-offset {
  margin-bottom: 4.5rem;
}
.nav-link.nuxt-link-exact-active {
  font-weight: bolder;
  color: white;
}
</style>
