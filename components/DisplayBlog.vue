<!-- © Markus Schiffer, June 2020 -->
<!-- This component displays blog posts. It used by both (albeit differently) home and blog pages. -->

<template>
  <!-- There were no errors loading the blog posts. -->
  <div v-if="!loadingBlogs && !errored">
    <!-- There exist posts to view. -->
    <div v-if="currPosts.length !== 0" class="container">
      <!-- Load in each post. Appropriately display everything that makes up a post. -->
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
    <!-- There has not yet been a post (ever). -->
    <div v-else class="container">
      <div class="card">
        <p class="card-text">
          There are no posts yet. Be the first to make a post!
        </p>
      </div>
    </div>
  </div>
  <!-- There was an error loading the blog posts. -->
  <div v-else-if="errored">
    <p>Sorry, it appears the API is not loading the blogs. {{ errorMessage }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'DisplayBlog',
  // Whether to only load the three newest posts or all of them.
  props: {
    unlimited: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      loadingBlogs: true, // The posts are currently being loaded.
      currPosts: [], // The posts to be displayed.
      errored: false, // There was an error getting the posts.
      errorMessage: '' // If there was an error, the error message goes here.
    }
  },
  mounted () {
    // Gets the blog posts.
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
        this.errorMessage = error
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
