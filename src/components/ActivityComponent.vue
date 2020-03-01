<template lang="html">
  <div class="">
    <div v-if="activity.activity">
      <h2>{{activity.activity}}</h2>
      <p>{{activity.type}}</p>
      <p>{{activity.participants}}</p>
      <p>{{activity.price}}</p>
      <p>{{activity.accessibility}}</p>
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
