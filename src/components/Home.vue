<template>
  <div>
    <h4>Serveurs : </h4>

            <ul>
                <li v-for="OneServer in ServerList">
                    <button @click="updateSelectedServer(OneServer)">{{OneServer.name}}</button>
                    <!--<input type="radio" class="radio-button" name="ServerButton" v-on:change="updateSelectedServer(OneServer)" >-->

                    <div v-for="item in LabelIdList">
                         <label v-if="testIdPresent(item,OneServer) === true"><input :id="item.id" :value="item.id" type="checkbox" v-model="CheckedList">{{ item.name }} </label>
                    </div>
                </li>

            </ul>
            <button @click="updateGraph(SelectedServer,CheckedList)">OK</button>
    <div id="app">
      <line-chart :data="data" />
    </div>
        </div>
    <graphic-detail></graphic-detail>
  </div>
</template>

<script>
    import ServerList from './ServerList.vue';
    import LabelList from './LabelList.vue';
    import axios from 'axios';
    import GraphicDetail from "./GraphicDetail.vue";

    export default {
  name: 'Home',
        components:{
            GraphicDetail,
            ServerList, LabelList},
  data () {
    return {
      CheckedList: [],
      CheckedServer: {},
      ServerList: [],
      LabelIdList: [],
      SelectedServer: null,
      items: [],
      errors: [],
      data: []
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
      },

      updateGraph: function (server,datas) {
        this.data = datas;
        console.log(server.id,datas);
      },

      updateSelectedServer: function (server) {
        this.SelectedServer = server;
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
