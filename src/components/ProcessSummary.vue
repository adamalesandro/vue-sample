<template>
    <div>
        <h1>{{process.processName}}</h1>
        <ProcessDetail :process='process' />
    </div>
</template>
<script>
import ProcessDetail from './ProcessDetail'
export default {
    props: {
        process: Object
    },
    components: {
        ProcessDetail
    }
}
</script>
