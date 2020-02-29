<template lang="html">
  <div>
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
