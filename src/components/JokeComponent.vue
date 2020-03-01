<template lang="html">
  <div>
    <h4 class="mb-3">Joke of the day</h4>
    <p>{{joke.setup}}</p>
    <p>{{joke.punchline}}</p>
  </div>
</template>

<script>
export default {
  name: 'joke-component',
  props: ['joke']
}
</script>

<style lang="css" scoped>
</style>
