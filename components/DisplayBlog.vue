<template>
  <div v-if="!loadingBlogs">
    <div v-if="currPosts.length !== 0" class="container">
      <div v-for="(post, index) in currPosts" :key="index" class="card mt-5 mb-5">
        <div class="card-header">
          <h3 class="card-title display-4">
            {{ post.title }}
          </h3>
          <h4 class="card-subtitle">
            {{ post.author }} posted at {{ post.time }}
          </h4>
        </div>
        <div class="card-body">
          <p class="card-text">
            {{ post.content }}
          </p>
        </div>
      </div>
    </div>
    <div v-else class="container">
      <div class="card">
        <p class="card-text">
          There are no posts yet. Be the first to make a post!
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'DisplayBlog',
  props: {
    unlimited: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      loadingBlogs: true,
      currPosts: [],
      errored: false
    }
  },
  mounted () {
    axios
      .get('http://markusschiffer.pythonanywhere.com/get-posts')
      .then((response) => {
        if (this.unlimited) {
          this.currPosts = response.data.posts
        } else {
          this.currPosts = response.data.posts.slice(0, 3)
        }
      })
      .catch((error) => {
        this.errored = true
        return Promise.reject(error)
      })
      .finally(() => (this.loadingBlogs = false))
  }
}
</script>

<style scoped>
.card {
  width: 100%;
  display: block;
}
</style>
