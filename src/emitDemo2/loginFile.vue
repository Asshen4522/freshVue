<script setup>
import { reactive } from 'vue';

const props = defineProps({
    records : Array
})
const emit = defineEmits([
    'loginEmit'
])

const local = reactive({
    inpName : ""
})
</script>
<template>
    <div>
        <div>
            <h2>Введите имя</h2>
            <input type="text" v-model="local.inpName">
            <button @click="$emit('loginEmit',local.inpName)">Отправить</button>
        </div>
        <div>
            <div v-for="elem in props.records">
                {{ elem.name }} : {{ elem.result }}
            </div>
        </div>
        
    </div>
</template>
<style scoped>
</style>
