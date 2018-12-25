<template>
  <div id="app">
    <QuerySeat />
  </div>
</template>

<script>
import QuerySeat from './components/QuerySeat.vue'

export default {
  name: 'app',
  components: {
    QuerySeat
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
