<script setup>
import { reactive } from "vue";
import register from "./login.vue";
import test from "./test.vue";
import display from './display.vue'
import modal from '../components/modal.vue'

const local = reactive({
    curPage : 1,
    users : [
    {
        name : "Раз",
        gender : "Мужчина",
        age : 23,
        results : [],
    },
    {
        name : "Два",
        gender : "Женщина",
        age : 17,
        results : [],
    },
    {
        name : "Три",
        gender : "Нечто",
        age : 64,
        results : [],
    }
    ],
    curUserIndex : "",

    modalShow: false,
    modalText : "",
})

function regEmit(data) {
    local.users.push(data)
    local.curUserIndex = local.users.length-1
}
function disEmit(data) {
    local.users.splice(data,1)
    if (local.curUserIndex>data) {
        local.curUserIndex-=1
    }else if (local.curUserIndex == data) {
        local.curUserIndex = ""
    }
}
function moveToTest() {
    if (!(local.curUserIndex === "")) {
        local.curPage = 3
    }else{
        local.modalShow = true
        local.modalText = "Авторизуйтесь"
    }
}
function checkAuth() {
    if (local.curUserIndex === "" && local.curPage == 3) {
        local.curPage = 1
        local.modalShow = true
        local.modalText = 'Вы не можете проходить тест без выбранного пользователя'
    }
}

</script>
<template>
    <div class="header">
        <div class="menu">
            <button @click="local.curPage = 1" :class="{menuItems : local.curPage==1}">Зарегистрировать пользователя</button>
            <button @click="local.curPage = 2" :class="{menuItems : local.curPage==2}">Вывод пользователей</button>
            <button @click="moveToTest" :class="{menuItems : local.curPage==3}">Пройти тест</button>
        </div>
        <select v-model="local.curUserIndex" @change="checkAuth">
            <option value="">Нет пользователя</option>
            <option :value="index" v-for="(elem,index) in local.users">{{ elem.name }}</option>
        </select>
    </div>
    
    <div>
        <register  
        v-if="local.curPage == 1"   
        @RegisterEmit="regEmit"/>
        <display 
        v-if="local.curPage == 2" 
        :users="local.users" 
        :curUser="local.curUserIndex"
        @deleteEmit="disEmit"/>
        <test 
        v-if="local.curPage == 3" 
        @TestEmit="(data)=>local.users[local.curUserIndex].results.push(data)"/>
    </div>

    <div>
        <modal 
        v-if="local.modalShow" 
        modalType="yes" 
        :modalText="local.modalText" 
        @modalYes="local.modalShow=false"/>
    </div>
    
</template>
<style scoped>
.header{
    display: flex;
    min-width: 1300px;
}
.menu{
    min-width: 1000px;
    display: flex;
    justify-content: space-around;
}
.menuItems{
    border-color: aqua;
    border-width: 5px;
}

</style>