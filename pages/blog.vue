<template>
  <div class="container">
    <h2 class="display-2 text-primary text-center">
      Blog
    </h2>
    <WriteBlog @handlePost="forceRender()" />
    <display-blog :key="renderKey" />
  </div>
</template>

<script>
import DisplayBlog from '../components/DisplayBlog.vue'
import WriteBlog from '../components/WriteBlog.vue'

export default {
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
    forceRender () {
      setTimeout(() => (this.renderKey += 1), 500)
    }
  }
}
</script>
