<!-- © Markus Schiffer, June 2020 -->
<!-- The main blog page. Includes the option to write a new post as well as view all previous blogs. -->

<template>
  <div class="container">
    <h2 class="display-2 text-primary text-center">
      Blog
    </h2>
    <!-- We need to re-render the page when a blog is posted, so the user can see instant results. -->
    <WriteBlog @handlePost="forceRender()" />
    <!-- Render key is a arbitrary number which informs display-blog to re-render when it becomes a different number -->
    <display-blog :key="renderKey" />
  </div>
</template>

<script>
import DisplayBlog from '../components/DisplayBlog.vue'
import WriteBlog from '../components/WriteBlog.vue'

export default {
  name: 'Blog',
  components: {
    DisplayBlog,
    WriteBlog
  },
  data () {
    return {
      renderKey: 0
    }
  },
  methods: {
    // Re-renders the display-blog, after enough time has passed for the backend to update the blog state.
    forceRender () {
      setTimeout(() => (this.renderKey += 1), 1000)
    }
  }
}
</script>
