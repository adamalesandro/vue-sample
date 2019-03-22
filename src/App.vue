<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light">OVER</span>
        <span>WATCH</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn small color="primary" @click="setFilter(null)">All</v-btn>
      <v-btn small color="success" @click="setFilter('Success')">Success</v-btn>
      <v-btn small color="error" @click="setFilter(['Failed', 'Error'])">Failed</v-btn>
    </v-toolbar>

    <v-content>
      <ul>
        <li v-for="process in filteredData" :key="process.processName">
        <ProcessSummary :process="process"/>
        </li>
      </ul>
    </v-content>
  </v-app>
</template>

<script>
import ProcessSummary from './components/ProcessSummary'

export default {
  name: 'App',
  components: {
    ProcessSummary
  },
  computed: {
        filteredData: function() {
            return this.processes.filter(obj => {
                if (this.statusFilter == null) {
                    return obj;
                }
                else
                    return this.statusFilter.includes(obj.status);
            });
        }
    },
    methods: {
        setFilter: function(filterInput) {
            this.statusFilter = filterInput;
        }
    },
  data () {
    return {
      statusFilter: null,
      processes: []
    }
  },
  created() {
    fetch("http://localhost:8888/api/data")
        .then(response => response.json())
        .then(json => { this.processes = json.data });
  }
}
</script>
