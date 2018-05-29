<template>
  <div>
    <h4>Labels : </h4>
    <div>
      <ul>
        <li v-for="item in items">
          <input :id="item.name" type="checkbox"> {{ item.name }}
        </li>
      </ul>
    </div>

    <ul v-if="errors && errors.length">
        <li v-for="error of errors">
          {{error.message}}
        </li>
      </ul>
  </div>
</template>

<script>
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
