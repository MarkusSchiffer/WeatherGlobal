<!-- © Markus Schiffer, June 2020 -->
<!-- This component allows the user to add their own blog posts. It is either an type-into interface or an expandable button. -->

<template>
  <!-- Click this button to access the new post interface. -->
  <b-button v-if="hide" variant="outline-primary w-100 mt-3" @click="toggleHide()">
    Add a post:
  </b-button>
  <!-- The form for a new blog. -->
  <form v-else ref="new.blog" class="jumbotron pt-4" @submit.prevent="getFormValues">
    <!-- Close button so that the user can close the interface if they want too. -->
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
      title: '', // The title of the blog post being written.
      author: '', // The author of the blog post being written.
      content: '', // The content of the blog post being written.
      hide: true // Whether to hide the form interface or not.
    }
  },
  methods: {
    // Flip whether to hide or show the form.
    toggleHide () {
      this.hide = !this.hide
    },
    // Valideate the form, ensure the user wants to post, and let the the server know about the new post.
    getFormValues () {
      const title = this.title
      const author = this.author
      const time = new Date().toLocaleString() // Get the time of the post.
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
      // Create a query string, this is how we send data to our server.
      const query = '?title=' + title + '&author=' + author + '&time=' + time + '&content=' + content
      query.replace(/ /g, '+')
      axios
        .get('https://cors-anywhere.herokuapp.com/http://markusschiffer.pythonanywhere.com/new-post' + query)
        .catch((error) => {
          this.errored = true
          alert('Blog failed to post, API error: ' + error)
        })
      this.$refs['new.blog'].reset() // clear the form upon posting.
      this.toggleHide() // hide the form interface upon posting, so the user can see the update.
      this.$emit('handlePost') // Event that tells the parent to refresh the page so that the new post is automatically displayed.
    }
  }
}
</script>
