<!-- © Markus Schiffer, June 2020 -->
<!-- The about me page. This page talks about the site and me, so potential employers can reach me. I opted not to load data
     from a json due to this pages simplicty, and trying to standardize each jumbotron was more work than it is worth. -->

<template>
  <div class="container lead">
    <h2 class="display-1 text-secondary text-center">
      About the Site!
    </h2>
    <div class="jumbotron">
      <img src="../static/markus.jpg" alt="Picture of the author.">
      <p>
        I'm Markus Schiffer. I created this site! I'm a UW CS student in the Allen School, and I live in the greater Seattle area. I have an intrest in computer security and systems programming. Some of my skills include Java, C++, Python, Vue,js, React.js, Ruby, Bootstrap, and Sass. If you like what you saw here, please don't hesitate to reach out! I'm always excited to hear about internship and job offers! My email is markus.mobx@gmail.com. Please check out my portfolio, it has some of my other projects as well the source code for this site!
        Thanks, Markus.
        <a href="https://drive.google.com/drive/u/0/folders/1ZHAzCGLB-XGfB65qFPXec0q3UUrEL-wN">My portfolio</a>
      </p>
    </div>
    <div class="jumbotron">
      <img src="../static/cloud.svg" alt="Website Cloud logo">
      <p>
        Cloud icon made by <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon"> www.flaticon.com</a>
      </p>
    </div>
    <div class="jumbotron">
      <img src="../static/icon.png" alt="Nuxt logo">
      <p>
        The front end of this webside was programmed in the Nuxt extension for the Vue.js Framework. It includes built in support for many more features out of the box than in the initial Vue.js packages. Unlike React or Angular, Vue is not maintained by a major tech company. Vue instead is maintained by dedicated community members. Vue actually tries to be a middle ground between the two other Frameworks, taking the best parts of both React and Angular and combining them into one.
      </p>
    </div>
    <div class="jumbotron">
      <img src="../static/flask-logo.png" alt="flask logo">
      <p>
        The backend for this website was a custom built flask api. This API is in charge of maintaining the blog posts. It stores posts both as a local dictionary object and backs it up in a database. So, when I said you cannot delete your posts, I hope you where listening!
      </p>
    </div>
    <div class="jumbotron">
      <img src="../assets/weathericons/lc.svg" alt="Metaweather logo">
      <p>
        This website uses the Metaweather API to load the weather forecases seen on the Home and Cities pages. This API allows to get the weather information (including information that not shown on this site) in a json format. It's also thanks to this site for the weather icons. Check them out here:
        <a href="https://www.metaweather.com/">MetaWeather</a>
      </p>
    </div>
    <div class="jumbotron">
      <img src="../static/logo.png" alt="Teleport logo">
      <p>
        The Teleport API provided the amazing pictures of the city skylines you see on this site. Check them out here:
        <a href="https://teleport.org/">Teleport</a>
      </p>
    </div>
    <div class="jumbotron">
      <img src="../static/bootstrap.png" alt="Bootstrap logo">
      <p>
        This site uses predominately Bootstap styles, with some custom CSS as well!
      </p>
    </div>
    <div class="jumbotron">
      <img src="../static/Globe.svg" alt="Wikipedia globe">
      <p>
        Globe images come from Wikimedia Commons. Check them out:
        <a href="https://commons.wikimedia.org/wiki/Main_Page">Wikimedia</a>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'About'
}
</script>

<style scoped>
.jumbotron {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  opacity: 0.75;
  transition: opacity .25s ease-in-out;
  -moz-transition: opacity .25s ease-in-out;
  -webkit-transition: opacity .25s ease-in-out;
}
  .jumbotron:hover {
    opacity: 1;
  }
.jumbotron img {
  max-width: 35%;
}
.jumbotron p {
  max-width: 55%;
}
</style>
