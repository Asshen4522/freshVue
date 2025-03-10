<script setup>
import { reactive } from 'vue';
import login from './loginFile.vue'
import test from './testFile.vue'

const local = reactive({
    curPage : true,
    curName : "",

    statistics : [],
})

function funLogin(logName) {
    local.curName = logName
    local.curPage = false
}
function funTest(records) {
    local.statistics.push(records)
    local.curPage = true
}
</script>

<template>
    <div>
        <login 
        v-if="local.curPage"
        :records="local.statistics"
        @loginEmit="funLogin"/>
        <test 
        v-if="!local.curPage"
        :testName="local.curName"
        @testEmit="funTest"/>
    </div>
</template>

<style scoped>
</style>