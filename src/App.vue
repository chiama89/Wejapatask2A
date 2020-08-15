<template>
  <div id="app">
    <countries msg="Wejapa Countries"/>
  </div>
</template>

<script>
import countries from './components/countries.vue'
export default {
  name: 'App',
  components: {
    countries
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
