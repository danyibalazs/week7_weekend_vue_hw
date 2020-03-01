<template lang="html">
  <div class="">
    <div v-if="activity.activity">
      <b-card>
        <h2>{{activity.activity}}</h2>
        <p>Type: {{activity.type}}</p>
        <p>Participants: {{activity.participants}}</p>
        <p>Price: {{activity.price}}</p>
        <p>Accessibility: {{activity.accessibility}}</p>
      </b-card>
    </div>

    <div v-if="activity.error">
      <h2>{{activity.error}}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: 'activity-component',
  props: ['activity']
}
</script>

<style lang="css" scoped>
</style>
