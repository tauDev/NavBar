<template>
 <div>
     <h1>Page NavBar</h1>
     <b-table striped hover
     :items="items"
     :current-page="currentPage"
     :per-page="perPage"></b-table>
     <div>
         <b-pagination :total-rows="totalRows" :per-page="perPage" v-model="currentPage" class="my-0"/>
     </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      items: [],
      currentPage: 1,
      perPage: 7,
      totalRows: 0
    }
  },
  mounted () {
    axios.get('http://192.168.0.124:3000/show').then(response => {
      this.items = response.data
      this.totalRows = response.length
    })
  }
}
</script>
