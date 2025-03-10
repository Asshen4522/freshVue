<script setup>
import { reactive } from 'vue';


const emit = defineEmits([
    'RegisterEmit'
])

const local = reactive({
    name : "",
    gender : "",
    age : "",

    nameError : false,
    genderError : false,
    ageError : false,

})

function check() {  
    let passCheck = true
    if (!/^[А-Я][а-я]+$/.test(local.name)) {
        local.nameError = true
        passCheck = false
    } else {
        local.nameError = false
    }
    if (!local.gender) {
        local.genderError = true
        passCheck = false
    } else {
        local.genderError = false
    }
    if (!(local.age<=100 && local.age>=5)) {
        local.ageError = true
        passCheck = false
    } else {
        local.ageError = false
    }

    if (passCheck) {
        emit('RegisterEmit',{
        name : local.name,
        gender : local.gender,
        age : local.age,
        results : [],
    })
        local.name = ""
         local.gender = ""
         local.age = ""
    }
    
}
</script>
<template>
    <div>
        <h2>Создание пользователя</h2>
        <div>
            <input type="text" placeholder="Имя" v-model="local.name">
            <div class="error" v-if="local.nameError">Введите имя одним словом с заглавной буквы</div>
            <div>
                <div>Пол</div>
                <div><input type="radio" value="Мужчина" id="gender-1" v-model="local.gender"><label for="gender-1">Мужской</label></div>
                <div><input type="radio" value="Женщина" id="gender-2" v-model="local.gender"><label for="gender-2">Женский</label></div>
                <div><input type="radio" value="Нечто" id="gender-3" v-model="local.gender"><label for="gender-3">Средний</label></div>
            </div>
            <div class="error" v-if="local.genderError">Вы кто?</div>
            <input type="number" placeholder="Возраст" v-model="local.age">
            <div class="error" v-if="local.ageError">Выберите адекватный возраст</div>
            <div>
                <button @click="check">Подтвердить</button>
            </div>
        </div>
    </div>
</template>
<style scoped>
.error{
    color: red;
}
</style>