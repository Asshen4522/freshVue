<script setup>
import { reactive } from 'vue';

const localStatic = reactive({
    countFilter: null,
    speedFilter: null,
    sizeFilter: null,
})

const props = reactive({
    messageSettings: [{
        count : 1,
        speed : 1,
        size : 1,
        res : 1,
    }],
})

</script>


<template>
    <h1>Статистика</h1>
    <div class="main">
        <table>
            <thead>
                <th>Количество целей</th>
                <th>Скорость целей</th>
                <th>Размер целей</th>
                <th>Результат</th>
            </thead>
            <tbody>
                <tr v-for="(elem) in props.messageSettings">
                    <template v-if="(!localStatic.countFilter || elem.count == localStatic.countFilter) && (!localStatic.speedFilter || elem.speed == localStatic.speedFilter) && (!localStatic.sizeFilter || elem.size == localStatic.sizeFilter)"
                    >
                        <td>{{ elem.count }}</td>
                        <td>{{ elem.speed }}</td>
                        <td>{{ elem.size }}</td>
                        <td>{{ elem.res }}</td>
                    </template>
                </tr>
            </tbody>
        </table>

        <div class="filtres">
            <div class="filter count">
                <h3>Фильтрация по количеству</h3>
                <label for="lot1"><input type="radio" name="forCount" value="15" id="lot1" v-model="localStatic.countFilter">15</label>
                <label for="middle1"><input type="radio" name="forCount" value="10" id="middle1" v-model="localStatic.countFilter">10</label>
                <label for="few1"><input type="radio" name="forCount" value="5" id="few1" v-model="localStatic.countFilter"> 5</label>
                <label for="not1"><input type="radio" name="forCount" value="" id="not1" v-model="localStatic.countFilter">Нет сортировки</label>
            </div>
            <div class="filter speed">
                <h3>Фильтрация по скорости</h3>
                <label for="quickly2"><input type="radio" name="forSpeed" value="5" id="quickly2" v-model="localStatic.speedFilter">5s</label>
                <label for="middle2"><input type="radio" name="forSpeed" value="7" id="middle2" v-model="localStatic.speedFilter">7s</label>
                <label for="gradually2"><input type="radio" name="forSpeed" value="10" id="gradually2" v-model="localStatic.speedFilter">10s</label>
                <label for="not2"><input type="radio" name="forSpeed" value="" id="not2" v-model="localStatic.speedFilter">Нет сортировки</label>
            </div>
            <div class="filter size">
                <h3>Фильтрация по размеру</h3>
                <label for="big3"><input type="radio" name="forSize" value="50" id="big3" v-model="localStatic.sizeFilter">Большой</label>
                <label for="middle3"><input type="radio" name="forSize" value="40" id="middle3" v-model="localStatic.sizeFilter">Средний</label>
                <label for="small3"><input type="radio" name="forSize" value="25" id="small3" v-model="localStatic.sizeFilter">Маленький</label>
                <label for="not3"><input type="radio" name="forSize" value="" id="not3" v-model="localStatic.sizeFilter">Нет сортировки</label>
            </div>
        </div>
    </div>   

</template>


<style scoped>
.main {
 display: grid;
 grid-template-columns: 1fr 1fr;
 gap: 10px;

}

table, th, td {
    width: 1000px;
    height: 50px;
    border: 2px solid #000;
    border-collapse: collapse;
}

.filtres {
    border: 1px solid #444;
}
.filter {
    display: flex;
    flex-direction: column;
    border: 1px solid #444;
}

.none {
    display: none;
}




</style>