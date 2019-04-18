<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ childMsg }}</h1>
    <h1>test1:{{ dataJson.test1 }}</h1>
    <h1>test2:{{ dataJson.test2 }}</h1>
    <button @click="changeF">子组件</button>
    <button @click="changeMyChildMsg()">自己修改</button>
  </div>
</template>

<script>
export default {
  name: 'Page',
  props: {
    msg: String,
    dataJson: {
      test1: 1,
      test2: 2
    }
  },
  data: function () {
    return {
      childMsg: null
    }
  },
  created: function () {
    console.log(111111111111)
  },
  beforeUpdate: function () {
    console.log(222222)
    console.log(this.dataJson)
    // this.childMsg = 'beforeUpdate'
    this.childMsg = 'beforeUpdate'
  },
  updated: function () {
    console.log('updated')
    console.log(this.dataJson)
  },
  methods: {
    changeF: function () {
      console.log('子组件单击开始')
      this.$emit('changeP')
    },
    changeMyChildMsg: function () {
      this.childMsg = +new Date()
    },
    parentHandleclick (e) {
      console.log(e)
      this.childMsg = e
    }
  },
  watch: {
    childMsg (newV, oldV) {
      console.log('ttttttttt')
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
