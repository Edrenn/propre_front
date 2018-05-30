<template>
  <div>
    <h4>Serveurs : </h4>

            <ul>
                <li v-for="OneServer in ServerList">
                    <button @click="updateSelectedServer(OneServer.id)">{{OneServer.name}}</button>
                    <!--<input type="radio" class="radio-button" name="ServerButton" v-on:change="updateSelectedServer(OneServer)" >-->

                    <div :id="OneServer.id" v-for="item in LabelIdList" v-if="serverId === OneServer.id">
                         <label v-if="testIdPresent(item,OneServer) === true"><input :id="item.id" :value="item.id" type="checkbox" v-model="labelIds">{{ item.name }} </label>
                    </div>
                </li>

            </ul>
    <div id="app">
    <div>
            <label>Date et heure de début du graph</label>
            <form>
                <input type="text" placeholder="DD/MM/AAAA hh:mm" v-model="timeStart">
                <label>Date et heure de fin du graph</label>
                <input type="text" placeholder="DD/MM/AAAA hh:mm" v-model="timeEnd">
            </form>
            <button type="submit" @click="getData(timeStart, timeEnd,labelIds)">Valider</button>
      <line-chart :data="data" />
    </div>
  </div>
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
      ServerList: [],
      LabelIdList: [],
      LeftSelected: false,
      items: [],
      errors: [],
      data: [],
      serverId: 0,
      labelIds: [],
      timeStart: "04/01/2018 00:01",
      timeEnd: "04/01/2018 01:11"
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

      updateSelectedServer: function (serverId) {
        if (this.serverId === serverId)
        {
          this.serverId = 0;
        }
        else
        {
          this.serverId = serverId;
        }
      },

      getData: function(timeStart, timeEnd,CheckedList) {
                      this.timeStart = timeStart;
                      this.timeEnd = timeEnd;
                      console.log(this.serverId);
                      axios.post('http://localhost:8080/data',
                          {
                              serverId : this.serverId,
                              labelIds : this.labelIds,
                              timeStart : this.timeStart,
                              timeEnd : this.timeEnd

                          }).then(res => {
                          this.data = res.data;
                      }).catch(e => {
                          this.errors.push(e);
                      })

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
