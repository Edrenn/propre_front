<template>
  <div>
    <h1>{{ msg }} {{title}}</h1>
    <h4>Serveurs : </h4>
    <ul>
      <li><a href="">Serveur 1</a></li>
      <li><a href="">Serveur 2</a></li>
    </ul>
    <div id="app">
      <line-chart :data="data" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      msg: 'Graph from server : ',
      title: 'srv-DC-london_global',
      data: [
        {
          name: 'cpu0',
          data: {
          '1515020486': 49.620000,
          '1515020786':62.420000,
          '1515021086': 47.970000
          }
        },
        {
          name: 'cpu1',
          data: {
          '1515020486': 60.310000,
          '1515020786':66.060000,
          '1515021086': 48.030000
          }
        }
      ]
    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
