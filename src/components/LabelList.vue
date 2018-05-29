<template>
  <div>
    <h4>Labels : </h4>
    <div>

      <form id="test">
        <div v-for="item in items">
          <input :id="item.name" type="checkbox"> {{ item.name }}
        </div>
        <input type="submit" onclick="myFunction()">
      </form>
      <!--<ul>
        <li v-for="item in items">
          <input :id="item.name" type="checkbox"> {{ item.name }}
        </li>
      </ul>-->
    </div>

    <ul v-if="errors && errors.length">
        <li v-for="error of errors">
          {{error.message}}
        </li>
      </ul>
  </div>
</template>

<script>
/*myFunction : function () {
    //window.alert(document.getElementById("test").submit());
       window.alert("oui");
   }*/

import axios from 'axios';



export default {
  name: 'labellist',
  data () {
    return {
      items: [],
      errors: []
    }
  },

  created() {
      axios.get(`http://localhost:8080/label`)
      .then(response => {
        // JSON responses are automatically parsed.
        this.items  = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })
      }


}
</script>
