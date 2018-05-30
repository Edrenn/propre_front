<template>
  <div id="app">
  <h1> GRAPH & FURIOUS 18 </h1>
    <img src="./assets/vindiesel.jpg">
    <Home/>
  </div>
</template>

<script>
import Home from './components/Home';
import Serverlist from './components/ServerList.vue';
import labellist from './components/LabelList.vue';

export default {
  name: 'App',
  components: {
      Home,
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
