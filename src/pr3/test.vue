<script setup>
import { reactive } from 'vue';
import modal from '../components/modal.vue';

const emit = defineEmits([
    'TestEmit'
])

const local = reactive({
    questions : [
        "Вопрос 1",
        "Вопрос 2",
        "Вопрос 3",
        "Вопрос 4",
        "Вопрос 5",
        "Вопрос 6",
        "Вопрос 7",
        "Вопрос 8",
        "Вопрос 9",
        "Вопрос 10",],
    models : ["","","","","","","","","","",],
    answers : ["1","2","3","4","5","6","7","8","9","10",],

    modalShow: false

})

function check() {
    let result = 0
    for (let index = 0; index < local.models.length; index++) {
        if (local.models[index]==local.answers[index]) {
            result+=1
        }
    }
    emit('TestEmit',result)
    for (let index = 0; index < local.models.length; index++) {
        local.models[index]=""
    }
}

function funYes() {
    local.modalShow = false
    check()
}
function funNo() {
    local.modalShow = false
}

function btnPush() {
    let noAnswers = true
    local.models.forEach(element => {
        if (!(element==="")) {
            noAnswers = false
        }
    });
    if (noAnswers) {
        local.modalShow = true
    }else{
        check()
    }
}

</script>
<template>
    <div>
        <h2>Пройдите тест</h2>
        <div class="questions">
            <div v-for="(elem,index) in local.questions">
                <div>{{elem}}</div>
                <input type="text" v-model="local.models[index]">
            </div>
        </div>
        <button @click="btnPush">Проверить</button>
        <div>
            <modal v-if="local.modalShow" modalType="answer" modalText="Вы не заполнили ответ ни на один вопрос. Хотите продолжить отправку?" @modalYes="funYes" @modalNo="funNo"/>
        </div>
    </div>
</template>
<style scoped>
.questions{
    display: flex;
    flex-direction: column;
    gap: 10px;
}
</style>