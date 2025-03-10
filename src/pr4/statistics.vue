<script setup>
import { reactive } from 'vue';

const props = defineProps({
    stats: Array
})
const local = reactive({
    chosenNum : 4,
    chosenSpeed : 4,
    chosenSize : 4,
})

</script>
<template>
    <div class="main">
        <div>
            <div class="stroka" >
                <div class="strokaEl">Количество целей</div>
                <div class="strokaEl">Скорость целей</div>
                <div class="strokaEl">Размер целей</div>
                <div class="strokaEl">Результат</div>
            </div>
            <div  v-for="elem in props.stats" >
                <div class="stroka" 
                v-if="((elem.num == local.chosenNum)||local.chosenNum==4)&&
                ((elem.speed == local.chosenSpeed)||local.chosenSpeed==4)&&
                ((elem.size == local.chosenSize)||local.chosenSize==4)">
                    <div class="strokaEl">{{ elem.num }}</div>
                    <div class="strokaEl">{{ elem.speed }}</div>
                    <div class="strokaEl">{{ elem.size }}</div>
                    <div class="strokaEl">{{ elem.result }}</div>
                </div>
            </div>
        </div>
        <div>
            <div>
                <h5>Сортировка по количеству</h5>
                <div><input type="radio" id="p1-1" value="3" v-model="local.chosenNum"><label for="p1-1">много</label></div>
                <div><input type="radio" id="p1-2" value="2" v-model="local.chosenNum"><label for="p1-2">средне</label></div>
                <div><input type="radio" id="p1-3" value="1" v-model="local.chosenNum"><label for="p1-3">мало</label></div>
                <div><input type="radio" id="p1-4" value="4" v-model="local.chosenNum"><label for="p1-4">нет сортировки</label></div>
            </div>
            <div>
                <h5>Сортировка по скорости</h5>
                <div><input type="radio" id="p2-1" value="3" v-model="local.chosenSpeed"><label for="p2-1">быстро</label></div>
                <div><input type="radio" id="p2-2" value="2" v-model="local.chosenSpeed"><label for="p2-2">средне</label></div>
                <div><input type="radio" id="p2-3" value="1" v-model="local.chosenSpeed"><label for="p2-3">медленно</label></div>
                <div><input type="radio" id="p2-4" value="4" v-model="local.chosenSpeed"><label for="p2-4">нет сортировки</label></div>
            </div>
            <div>
                <h5>Сортировка по размеру</h5>
                <div><input type="radio" id="p3-1" value="3" v-model="local.chosenSize"><label for="p3-1">большой</label></div>
                <div><input type="radio" id="p3-2" value="2" v-model="local.chosenSize"><label for="p3-2">средний</label></div>
                <div><input type="radio" id="p3-3" value="1" v-model="local.chosenSize"><label for="p3-3">маленький</label></div>
                <div><input type="radio" id="p3-4" value="4" v-model="local.chosenSize"><label for="p3-4">нет сортировки</label></div>
            </div>
        </div>
        
    </div>
</template>
<style scoped>
.main{
    display: flex;
    flex-direction: row;
    gap: 20px;
    width: 1400px;
}
.stroka{
    height: 50px;
    display: grid;
    grid-template-columns: repeat(3,1fr) 2fr;
}
.strokaEl{
    border: 1px solid;
    padding: 10px;
}
</style>