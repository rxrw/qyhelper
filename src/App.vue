<template>
  <div id="app">
    <div class="container">
      <SpeedCalculator />
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

import SpeedCalculator from "./components/SpeedCalculator";

export default {
  name: 'app',
  components: {
    // HelloWorld,
    SpeedCalculator
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
