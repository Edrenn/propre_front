<template>
  <div>
    <h4>Serveurs : </h4>
        <form>
            <ul>
                <li v-for="OneServer in ServerList">
                    <input type="radio" class="radio-button" v-model="OneServer.id" name="ServerButton" >
                    {{OneServer.name}}
                    <div v-for="item in LabelIdList">
                         <label v-if="testIdPresent(item,OneServer) === true"><input :id="item" type="checkbox">{{ item.name }} </label>
                    </div>
                </li>
            </ul>
                    <input type="submit">
        </form>
    <div id="app">
      <line-chart :data="data" />
    </div>
  </div>
</template>

<script>
    import ServerList from './ServerList.vue';
    import LabelList from './LabelList.vue';
    import axios from 'axios';

    export default {
  name: 'Home',
        components:{ServerList, LabelList},
  data () {
    return {
      ServerList: [],
      LabelIdList: [],
      OneServer: {
          id: 0,
          name :'',
          LabelIdList:[]
      },
      items: [],
      errors: [],
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
  },
  mounted(){
              this.getServers();
          },

  methods:{
      getServers: function () {

          axios.get('http://127.0.0.1:8080/server')
              .then(res =>
                  this.ServerList = res.data,
              ).catch(e => {
              this.errors.push(e);
          })

      },

      testIdPresent: function (idTest,OneServer) {
        if (OneServer.labelId.indexOf(idTest.id) === -1)
        {
          return false;
        }
        else{
          return true;
        }
      }
  },

  created() {
        axios.get(`http://localhost:8080/label`)
        .then(response => {
          // JSON responses are automatically parsed.
          this.LabelIdList  = response.data
        })
        .catch(e => {
          this.errors.push(e)
        })
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
