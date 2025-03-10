<script setup>
import menuV from "./menu.vue";
import game from "./game.vue";
import settings from "./settings.vue";
import statistics from "./statistics.vue";
import { reactive } from "vue";


const local = reactive({
    curPage: 2,
    sett: {
        num: 2,
        speed: 2,
        size: 2,
    },
    statistic: []
})

function changeSet(par, num) {
    switch (par) {
        case 'num':
            local.sett.num = num
            break;
        case 'speed':
            local.sett.speed = num
            break;
        case 'size':
            local.sett.size = num
            break;
    }
}

function addStats(res) {
    local.statistic.push({
        num: local.sett.num,
        speed: local.sett.speed,
        size: local.sett.size,
        result: res,
    })
}
</script>
<template>
    <div>
        <header>
            <menuV @changePage="(page) => local.curPage = page" />
        </header>
        <main>
            <settings v-if="local.curPage == 1" :oldSet="local.sett" @setEmit="changeSet" />
            <game v-if="local.curPage == 2" :settings="local.sett" @endGame="addStats" />
            <statistics v-if="local.curPage == 3" :stats="local.statistic" />
        </main>
    </div>

</template>
<style scoped>
header {
    width: 800px;
    margin-bottom: 50px;
}
</style>