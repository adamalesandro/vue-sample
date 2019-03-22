<template>
  <v-layout>
    <v-flex xs12 sm6 offset-sm3>
      <v-card class="mt-2">
        <v-card-title>
          <div>
            <span class="display-2">{{process.processName}}</span>
          </div>
        </v-card-title>
        <v-card-text>
            <ProcessDetail :process="process" />
        </v-card-text>
        <v-card-actions>
          <v-btn flat color="orange" @click="dismiss">Dismiss</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>
<script>
import ProcessDetail from './ProcessDetail'
export default {
    props: {
        process: Object
    },
    components: {
        ProcessDetail
    },
    methods: {
        dismiss: function(){
            this.$emit('deleted', this.process);
        }
    }
}
</script>
