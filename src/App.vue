<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light">OVER</span>
        <span>WATCH</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn small flat color="primary" @click="setFilter(null)">All</v-btn>
      <v-btn small flat color="success" @click="setFilter('Success')">Success</v-btn>
      <v-btn small flat color="error" @click="setFilter(['Failed', 'Error'])">Failed</v-btn>
    </v-toolbar>

    <v-content>
        <div v-for="process in filteredData" :key="process.processName">
        <ProcessSummary :process="process" @deleted="onDeleteChild" />
        </div>
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
        },
        onDeleteChild: function(value) {
          this.processes.splice(this.processes.indexOf(value), 1);
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
