<template lang="html">
  <div>

    <h4 class="mb-3">Get a random activity:</h4>
    <b-button class="mb-3" @click="getRandomActivity">Random Activity</b-button>

    <h4 class="mb-3">Or get a specified one:</h4>
    <b-form @submit.prevent="getFilteredActivity">

      <b-form-group label="Type">
        <b-form-select size="sm" required v-model="selectedType" id="types">
            <option v-for="type in activityTypes" :value="type">{{type.toUpperCase()}}</option>
          </b-form-select>
      </b-form-group>

      <b-form-group label="Participans">
        <b-form-input  required placeholder="Number of participants" type="number" v-model.number="participants"></b-form-input>
      </b-form-group>

      <b-form-group label="Price">
        <b-form-radio-group>
        <b-form-radio required name="price" value="cheap" v-model="price">Cheap</b-form-radio>
        <b-form-radio name="price" value="expensive" v-model="price">Expensive</b-form-radio>
        </b-form-radio-group>
      </b-form-group>

      <b-form-group label="Accessibility">
        <b-form-radio-group>
        <b-form-radio required name="accessibility" value="easy" v-model="accessibility">Easy</b-form-radio>
        <b-form-radio nname="accessibility" value="hard" v-model="accessibility">Hard</b-form-radio>
        </b-form-radio-group>
      </b-form-group>

      <b-button type="submit">Get activity</b-button>

    </b-form>
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
