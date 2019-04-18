<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ childMsg }}</h1>
    <button @click="changeF">子组件</button>
  </div>
</template>

<script>
export default {
  name: 'Page',
  props: {
    msg: String
  },
  data: function () {
    return {
      childMsg: null
    }
  },
  methods: {
    changeF: function () {
      console.log('子组件单击开始')
      this.$emit('changeP')
    },
    parentHandleclick (e) {
      console.log(e)
      this.childMsg = e
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
