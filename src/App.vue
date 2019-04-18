<template>
  <div id="app" class="test-app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Pageination />
  </div>
</template>

<script>
import Pageination from './components/common/Pageination.vue'

export default {
  name: 'app',
  components: {
    Pageination
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
