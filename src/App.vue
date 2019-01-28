<template>
  <div id="app">
    <img src="./assets/logo.png">
    <form v-on:submit.prevent="doSubmit">
      <input type="text" v-model="data">
      <button type="submit">test</button>
    </form>
    <tr v-for="item in buttons">
      <td class="button">
        <button v-on:click="item.func">{{ item.data }}</button>
      </td>
    </tr>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  methods: {
    doSubmit: function(event, value) {
      console.log(this.data)
      var data = this.data
      this.buttons.push({
        data: data,
        func: function() {
          console.log(data)
        }
      })
      this.data = ''
    }
  },
  data () {
    return {
      data: '',
      buttons: []
    }
  },
  components: {
    HelloWorld
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
