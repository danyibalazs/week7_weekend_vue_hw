<template>

  <div id="app">

    <div>
      <b-jumbotron header="A Boring Joke App" lead="If you are bored here are some random activities...">
      <p>...and some jokes</p>
      </b-jumbotron>
    </div>

    <b-container>
      <b-row>
        <b-col><activity-form></activity-form></b-col>
        <b-col><activity-component :activity='randomActivity'></activity-component></b-col>
        <b-col><joke-component :joke='joke'></joke-component></b-col>
      </b-row>
    </b-container>
    
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
          activity.accessibility = 'HARD'
        };
        activity.type = activity.type.toUpperCase()
      }
    }
  }
}
</script>

<style>

</style>
