<script setup>
import { onMounted, onUnmounted, reactive } from 'vue';
import modal from "../components/modal.vue";

const emit = defineEmits([
    'endGame'
])
const props = defineProps({
    settings: Object
})

const local = reactive({
    targets: [],
    result: 50,
    interval: null,
    timer: null,
    catched: 0,
    started: false,

    modalShow: false,
    modalText: "",
})

function catching(index) {
    local.targets[index].display = 'none'
    local.result += 5
    local.catched += 1
    if (local.catched == props.settings.num * 5) {
        clearInterval(local.interval)
        clearInterval(local.timer)
        local.timer = null
        local.interval = null

        local.started = false
        local.targets = []

        local.modalShow = true
        local.modalText = `Вы победили, ваш результат: ${local.result}`
        emit('endGame', local.result)
    }

}

function startRace() {
    if (!local.started) {
        for (let index = 0; index < props.settings.num * 5; index++) {
            local.targets.push({
                display: 'block',
                transform: `translateX(${Math.random() * 750}px) translateY(${Math.random() * 825}px)`,
            })
        }

        local.interval = setInterval(changePos, 1400 - (200 * props.settings.speed))
        local.timer = setInterval(changeTime, 1000)
        local.started = true
        local.catched = 0
        local.result = 50
    }

}

function changePos() {
    local.targets.forEach(element => {
        element.transform = `translateX(${Math.random() * 750}px) translateY(${Math.random() * 825}px)`
    });
}
function changeTime() {
    local.result -= 1
    if (local.result == 0) {
        clearInterval(local.interval)
        clearInterval(local.timer)
        local.timer = null
        local.interval = null
        local.started = false
        local.targets = []

        local.modalShow = true
        local.modalText = `Увы, но вы проиграли`
        emit('endGame', local.result)
    }
}

// onMounted(() => console.log("Я родился"))
// onUnmounted(() => {
//     if (!local.timer) {
//         clearInterval(local.interval)
//         clearInterval(local.timer)
//     }
// })

</script>
<template>
    <div>
        <div class="field">
            <button :class="{
                target: true,
                target_small: props.settings.size == 1,
                target_medium: props.settings.size == 2,
                target_huge: props.settings.size == 3,
            }" v-for="(elem, index) in local.targets" @click="catching(index)" :style="elem">Тык</button>
        </div>
        <button @click="startRace">Начать</button>
        {{ local.result }}
        <div>
            <modal v-if="local.modalShow" modalType="yes" :modalText="local.modalText"
                @modalYes="local.modalShow = false" />
        </div>
    </div>
</template>
<style scoped>
.field {
    width: 900px;
    height: 900px;
    border-radius: 20px;
    border-style: solid;
    margin: 20px;
    text-align: start;
}

.target {
    position: absolute;
    background-color: blue;

    transition: 1.1s ease-in-out
}

.target_small {
    width: 50px;
    height: 25px;
    padding: 0;
}

.target_medium {
    width: 100px;
    height: 50px;
}

.target_huge {
    width: 150px;
    height: 75px;
}
</style>