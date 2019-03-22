<template>
    <div>
        <span class="display-1" :style="statusColor">{{process.status}}</span>
        <div v-if="hasLogData">
            <p>Log Data:</p>
            <ul>
                <li v-for="logEntry in process.logEntries" :key="logEntry.timestamp">
                    [{{logEntry.timestamp}}] {{logEntry.logData}}
                </li>
            </ul>
        </div>
        <div v-else>
            <p><em>No Log Data</em></p>
        </div>
    </div>
</template>

<script>
export default {
    computed: {
        hasLogData: function() {
            return !this.process.logEntries.length == 0;
        },
        statusColor: function() {
            if (this.process.status == "Failed")
                return "color: red";
            if (this.process.status == "Error")
                return "color: red";
            else
                return "color: green";
            },
    },
    props: {
        process: Object
    }
}
</script>
