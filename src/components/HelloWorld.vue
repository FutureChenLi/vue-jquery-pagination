<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <button v-on:click="changeMsg">测试</button>
      <button v-on:click="clickParent">调用子组件方法</button>
    </p>
    <h3>Installed CLI Plugins</h3>
    <Page @changeP="changeMsg" ref="myChild" v-bind:msg="myMsg"/>
  </div>
</template>

<script>
import Page from './common/Page.vue'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
    Page
  },
  data: function () {
    return {
      myMsg: null
    }
  },
  methods: {
    changeMsg () {
      console.log('父组件方法')
      if (this.myMsg == null) {
        this.myMsg = 'tttt'
      } else {
        this.myMsg = '测试'
      }
    },
    clickParent () {
      this.$refs.myChild.parentHandleclick('我是爸爸')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
