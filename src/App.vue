<template>
  <div id="app">
    <img src="./assets/logo.png">
    <labellist/>
  </div>
</template>

<script>
import labellist from './components/LabelList'

export default {
  name: 'App',
  components: {
    labellist
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
