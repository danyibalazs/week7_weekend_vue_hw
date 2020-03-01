<template lang="html">
  <div>
    <input @click="getRandomActivity" type="button" value="Random Activity">
    <form @submit.prevent="getFilteredActivity">
      <label for="types">Choose a type:</label>
      <select required v-model="selectedType" id="types">
            <option v-for="type in activityTypes" :value="type">{{type.toUpperCase()}}</option>
      </select>

      <label for="participants">Participants</label>
      <input required type="number" v-model.number="participants">
      <br>

      <label>Price</label>
      <br>
      <input required type="radio" name="price" value="cheap" v-model="price">
      <label>Cheap</label>
      <input type="radio" name="price" value="expensive" v-model="price">
      <label>Expensive</label>
      <br>

      <label>Accessibility</label>
      <br>
      <input required type="radio" name="accessibility" value="easy" v-model="accessibility">
      <label>Easy</label>
      <input type="radio" name="accessibility" value="hard" v-model="accessibility">
      <label>Hard</label>
      <br>

      <input type="submit" value="Get Activity">

    </form>
  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: 'activity-form',
  data(){
    return {
      activityTypes: ["education", "recreational", "social", "diy", "charity", "cooking", "relaxation", "music", "busywork"],
      selectedType: "",
      participants: null,
      price: "",
      accessibility: "",
      randomActivity: {}
    }
  },
    methods: {
      getRandomActivity(){
        fetch('http://www.boredapi.com/api/activity')
          .then(response => response.json())
          .then(data => {this.randomActivity = data;
            eventBus.$emit("randomActivity", this.randomActivity);
          });
      },
      getFilteredActivity(){
        let url = 'http://www.boredapi.com/api/activity'
          url += `?type=${this.selectedType}`;
          url += `&participants=${this.participants}`;
          if (this.price === 'cheap') {
            url += `&minprice=0&maxprice=0.5`;
          } else {
            url += `&minprice=0.51&maxprice=1`;
          };
          if (this.accessibility === 'easy') {
            url += `&minaccessibility=0&maxaccessibility=0.5`;
          } else {
            url += `&minaccessibility=0.51&maxaccessibility=1`;
          };
        fetch(url)
          .then(response => response.json())
          .then(data => {this.randomActivity = data;
            eventBus.$emit("randomActivity", this.randomActivity);
          });
      }
    }
  }

</script>

<style lang="css" scoped>
</style>
