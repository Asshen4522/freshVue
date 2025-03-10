<script setup>
import { reactive } from 'vue';

const props = defineProps({
    users : Array,
    curUser : ""
})
const emit = defineEmits([
    'deleteEmit'
])
const local = reactive({
    userRes : []
})

function genAverage() {
    console.log('res');
    
    local.userRes = []
    props.users.forEach(element => {
    let summ = 0
    element.results.forEach(smth => {
        summ+=smth
    })
    local.userRes.push(summ/element.results.length)
});
}





function del(index) {
    
    emit('deleteEmit',index)
    genAverage()
}
genAverage()
</script>
<template>
<div class="panel">
    <div class="card" :class="{active : index === props.curUser}" v-for="(elem,index) in props.users">
        <div class="cardSect">
            <div>{{ index+1 }} : {{elem.name}}</div>
            <button @click="del(index)">Удалить</button>
        </div>
        <div class="cardSectMid">
            <div>{{ elem.gender }}</div>
            <div>{{ elem.age }}</div>
        </div>
        <div class="cardSect" v-if="local.userRes[index] >=0">
            {{ local.userRes[index] }}
        </div>
        <div class="cardSect" v-else>
            Тест не проходился
        </div>
    </div>
</div>
</template>
<style scoped>
.panel{
    margin-top: 50px;
    width: 100%;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 20px;
}
.card{
    width: 200px;
    height: 200px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 30px;
    border: 2px solid;
    border-radius: 10px;
}
.active{
    background-color: aqua;
    border-color: blue;
}
.cardSect{
    display: flex;
    flex-direction: row;
    width: 100%;
    justify-content: space-between;
}
.cardSectMid{
    display: flex;
    flex-direction: row;
    width: 100%;
    justify-content: space-around;
}
</style>