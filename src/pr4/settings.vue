<script setup>
import { onMounted, onUnmounted, reactive } from 'vue';
const props = defineProps({
    oldSet: Object
})
const emit = defineEmits([
    'setEmit'
])

const local = reactive({
    numTargets: 1,
    speedTargets: 1,
    sizeTargets: 1,
})

function pickOption(param, num) {
    switch (param) {
        case 'num':
            local.numTargets = num
            break;
        case 'speed':
            local.speedTargets = num
            break;
        case 'size':
            local.sizeTargets = num
            break;
    }
    emit('setEmit', param, num)
}

local.numTargets = props.oldSet.num
local.speedTargets = props.oldSet.speed
local.sizeTargets = props.oldSet.size

onMounted(() => {
    console.log('Я родился')
})
onUnmounted(() => {
    console.log('Я умер')
})
</script>
<template>
    <div class="container">
        <div class="list">
            <h2>Количество целей</h2>
            <button @click="pickOption('num', 1)" :class="{ active: local.numTargets == 1 }">5</button>
            <button @click="pickOption('num', 2)" :class="{ active: local.numTargets == 2 }">10</button>
            <button @click="pickOption('num', 3)" :class="{ active: local.numTargets == 3 }">15</button>
        </div>
        <div class="list">
            <h2>Скорость целей</h2>
            <button @click="pickOption('speed', 1)" :class="{ active: local.speedTargets == 1 }">Низкая</button>
            <button @click="pickOption('speed', 2)" :class="{ active: local.speedTargets == 2 }">Средняя</button>
            <button @click="pickOption('speed', 3)" :class="{ active: local.speedTargets == 3 }">Высокая</button>
        </div>
        <div class="list">
            <h2>Размер целей</h2>
            <button @click="pickOption('size', 1)" :class="{ active: local.sizeTargets == 1 }">Небольшой</button>
            <button @click="pickOption('size', 2)" :class="{ active: local.sizeTargets == 2 }">Средний</button>
            <button @click="pickOption('size', 3)" :class="{ active: local.sizeTargets == 3 }">Крупный</button>
        </div>
    </div>
</template>
<style scoped>
.container {
    width: 100%;
    height: 100%;

    display: flex;
    flex-direction: row;
    justify-content: space-around;
}

.list {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.active {
    background-color: purple;
    color: wheat
}
</style>