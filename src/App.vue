<template>
  <div id="app">
    <!-- <joke-component :joke='joke'></joke-component> -->
  </div>
</template>

<script>
import JokeComponent from './components/JokeComponent.vue'

export default {
  name: 'App',
  components: {
    'joke-component': JokeComponent
  },
  data(){
    return {
      joke: {}
    }
  },
  mounted(){
    fetch("https://official-joke-api.appspot.com/jokes/programming/random")
    .then(response => response.json())
    .then(jokeData => {
      this.joke = jokeData[0];

    })
  }
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}
</style>
