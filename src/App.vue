<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Shortener />
  </div>
</template>

<script>
import Shortener from './components/shortener.vue'

export default {
  name: 'App',
  components: {
    Shortener,
  },
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
