<script setup>
import { reactive } from 'vue';

const emit = defineEmits([
    'testEmit'
])
const props = defineProps({
    testName : String
})
const local = reactive({
    q1 : "",
    q2 : "",
    q3 : "",
    q4 : null,
})

function check() {
    let result = 0 
    if (local.q1 == "1") {
        result +=1
    }
    if (local.q2 == "2") {
        result +=1
    }
    if (local.q3 == "3") {
        result +=1
    }
    result += Number(local.q4)
    emit('testEmit',{
        name : props.testName,
        result : result
    })
}
</script>
<template>
    <div>
        <h2> Приветствую, {{ props.testName }}</h2>
        <div>
            <div>Вопрос 1</div>        
            <input type="text" v-model="local.q1">
        </div>
        <div>
            <div>Вопрос 2</div>        
            <input type="text" v-model="local.q2">
        </div>
        <div>
            <div>Вопрос 3</div>        
            <input type="text" v-model="local.q3">
        </div>
        <div>
            <div>Вопрос 4</div>
            <div>
                <input type="radio" value="000" id="q4-1" v-model="local.q4"><label for="q4-1">Вариант 1</label>
                <input type="radio" value="1" id="q4-2" v-model="local.q4"><label for="q4-2">Вариант 2</label>
                <input type="radio" value="0" id="q4-3" v-model="local.q4"><label for="q4-3">Вариант 3</label>
                <input type="radio" value="00" id="q4-4" v-model="local.q4"><label for="q4-4">Вариант 4</label>
            </div>
        </div>
        <button @click="check">Проверить</button>
    </div>
</template>
<style scoped>
</style>