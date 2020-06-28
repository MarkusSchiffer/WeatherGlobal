<template>
  <b-button v-if="hide" variant="outline-primary w-100 mt-3" @click="toggleHide()">
    Add a post:
  </b-button>
  <form v-else ref="new.blog" class="jumbotron pt-4" @submit.prevent="getFormValues">
    <button type="button" class="close" aria-label="Close" @click="toggleHide()">
      <span aria-hidden="true">&times;</span>
    </button>
    <h2>Add a Post</h2>
    <div class="form-group">
      <label for="post-title">Post title:</label>
      <input id="post-title" v-model="title" type="text" class="form-control" placeholder="Creative post title here:">
    </div>
    <div class="form-group">
      <label for="post-author">Author's name:</label>
      <input id="post-author" v-model="author" type="text" class="form-control" placeholder="Your name here:">
    </div>
    <div class="form-group">
      <label for="post-content">Post content:</label>
      <textarea id="post-content" v-model="content" class="form-control" rows="6" placeholder="Write your thoughts here:" />
    </div>
    <button class="btn btn-primary" type="submit">
      Submit Post
    </button>
  </form>
</template>

<script>
import axios from 'axios'

export default {
  name: 'WriteBlog',
  data () {
    return {
      title: '',
      author: '',
      content: '',
      hide: true
    }
  },
  methods: {
    toggleHide () {
      this.hide = !this.hide
    },
    getFormValues () {
      const title = this.title
      const author = this.author
      const time = new Date().toLocaleString()
      const content = this.content
      if (title === '') {
        alert('ERROR: You must have a title!')
        return
      }
      if (author === '') {
        alert("ERROR: You must provide an author's name (use anonomous if you wish to stay anonomous)!")
        return
      }
      if (content === '') {
        alert('ERROR: Your post must have content!')
        return
      }
      if (!confirm('Are you sure you would like to post (you cannot delete a post)?')) {
        return
      }
      const query = '?title=' + title + '&author=' + author + '&time=' + time + '&content=' + content
      query.replace(/ /g, '+')
      axios
        .get('https://cors-anywhere.herokuapp.com/http://markusschiffer.pythonanywhere.com/new-post' + query)
        .catch((error) => {
          this.errored = true
          return Promise.reject(error)
        })
      this.$refs['new.blog'].reset()
      this.toggleHide()
      this.$emit('handlePost')
    }
  }
}
</script>
