<template>
  <navBar/>
  <br>
  <video id="video" autoplay controls disablepictureinpicture controlslist="nofullscreen nodownload noremoteplayback noplaybackrate">
    <source src="https://file-examples.com/storage/fe2879c03363c669a9ef954/2017/04/file_example_MP4_1280_10MG.mp4" type="video/mp4">
  </video>  
  <Survey msg="Queremos saber..."/>
</template>

<script>
import Survey from './components/Survey.vue'
import navBar from './components/navBar.vue';

export default {
  name: 'App',
  components: {
    Survey,
    navBar
  }
}
</script>

<style>


@media only screen and (max-width: 700px) {
  #video {
    width: 100% !important;
  }
}
#video {
  object-fit: cover;
  width: 80%;
  height: 600px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
