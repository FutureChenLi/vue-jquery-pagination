<template>
  <div id="app" class="test-app">
    <img alt="Vue logo" src="./assets/logo.png">
    <button @click="changeDataJson()">监听</button>
    <Pageination />
    <Page :msg="test" :data-json="dataJson"></Page>
  </div>
</template>

<script>
import Pageination from './components/common/Pageination.vue'
import Page from './components/common/Page.vue'

export default {
  name: 'app',
  components: {
    Pageination, Page
  },
  data: function () {
    return {
      dataJson: {
        test1: 1,
        test2: 2
      },
      test: '123'
    }
  },
  methods: {
    changeDataJson: function () {
      // this.dataJson = {
      //   test1: 2222,
      //   test2: 3333
      // }
      this.dataJson.test1 = 'aaaaaaa'
    }
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
