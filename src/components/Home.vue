<template>
  <div>
    <div class="title">
      <nav class="navbar navbar-light bg-light">
        <input
          class="form-control form-control-sm mr-sm-2 ml-4"
          @keyup="onSearch"
          v-model="searchString"
          type="text"
          placeholder="Search"
          aria-label="Search"
        >
      </nav>
    </div>
    <div class="main">
      <table class="table table-striped table-sm" v-if="tableData.length">
        <thead>
          <tr>
            <th data-text="sr">Sr.</th>
            <th data-text="title">Title</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, i) in tableData" :key="row.title">
            <td>{{i+1}}</td>
            <td>{{row.title}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      searchString: "",
      filteredData: [],
      tableData: []
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      let oConfig = {
        "access-control-allow-origin": "*",
        "access-control-allow-methods": "GET, POST, PUT",
        "access-control-allow-headers":
          "Origin, X-Requested-With, Content-Type, Accept",
        server: "cloudflare-nginx"
      };
      axios
        .get(`http://starlord.hackerearth.com/gamesext`, { header: oConfig })
        .then(response => {
          console.log(response);
        })
        .catch(oError => {
          console.log(oError);
        });
    },
    onSearch() {}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
