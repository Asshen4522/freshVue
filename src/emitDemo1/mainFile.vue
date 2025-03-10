<script setup>
import { reactive } from 'vue';
import comp from './notMain.vue';
const local = reactive({
    per : ""
})
function funEmit(params) {
    local.per = params
}
</script>
<template>
<comp @actionOne="funEmit" />
{{ local.per }}
</template>
<style scoped>
</style>