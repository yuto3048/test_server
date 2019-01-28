<template>
  <div id="app">
    <img src="./assets/logo.png">
    <form v-on:submit.prevent="doSubmit">
      <input type="text" v-model="name" placeholder="Name"><br>
      <input type="text" v-model="url" placeholder="URL"><br>
      <input type="text" v-model="param" placeholder="Param">
      <input type="text" v-model="param_data" placeholder=" Value"><br>
      <button type="submit">test</button>
    </form>
    <tr v-for="item in buttons">
      <td class="button">
        <button v-on:click="item.func">{{ item.name }}</button>
      </td>
    </tr>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import axios from 'axios'

export default {
  name: 'App',
  methods: {
    doSubmit: function(event, value) {
      var name = this.name
      var url = this.url
      var params = new URLSearchParams()
      params.append(this.param, this.param_data)
      this.buttons.push({
        name: name,
        url: url,
        params: params,
        func: function() {
          console.log(url)
          axios.post(url, params).then(response => {
            if (response.status === 200) {
              console.log('success')
              console.log(response.status)
            } else {
              console.log('error')
              console.log(response.status)
            }
          })
        }
      })
      this.name = ''
      this.url = ''
      this.param = ''
      this.param_data = ''
    }
  },
  data () {
    return {
      name: '',
      url: '',
      param: '',
      param_data: '',
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
