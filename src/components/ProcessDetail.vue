<template>
    <div>
        <span>Status: <strong>{{process.status}}</strong></span>
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
        }
    },
    props: {
        process: Object
    }
}
</script>
