<template>
  <div id="app">
    <activity-form></activity-form>
    <activity-component :activity='randomActivity'></activity-component>
    <joke-component :joke='joke'></joke-component>
  </div>
</template>

<script>
import JokeComponent from './components/JokeComponent.vue'
import ActivityForm from './components/ActivityForm.vue'
import ActivityComponent from './components/ActivityComponent.vue'
import {eventBus} from "./main.js"

export default {
  name: 'App',
  components: {
    'joke-component': JokeComponent,
    'activity-form': ActivityForm,
    'activity-component': ActivityComponent
  },
  data(){
    return {
      joke: {},
      randomActivity: {}
    }
  },
  mounted(){
    fetch("https://official-joke-api.appspot.com/jokes/programming/random")
    .then(response => response.json())
    .then(jokeData => {
      this.joke = jokeData[0];
    })

    eventBus.$on("randomActivity", (activity) => {
      this.randomActivity = activity;
      this.transformActivity(this.randomActivity);
    })
  },
  methods: {
    transformActivity(activity){
      if(!activity.error){
        if (activity.price <= 0.5) {
          activity.price = 'CHEAP'
        } else {
          activity.price = 'EXPENSIVE'
        };
        if (activity.accessibility <= 0.5) {
          activity.accessibility = 'EASY'
        } else {
          activity.accessibility = 'HARDER'
        };
        activity.type = activity.type.toUpperCase()
      }
    }
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
