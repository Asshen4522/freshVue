<script setup>
const emit = defineEmits([
    'changePage'
])
</script>
<template>
    <div class="menu">
        <button @click="$emit('changePage', 1)">Настройки</button>
        <button @click="$emit('changePage', 2)">Игра</button>
        <button @click="$emit('changePage', 3)">Статистика</button>
    </div>
</template>
<style scoped>
.menu{
    width: 100%;
    display : flex;
    flex-direction: row;
    justify-content: space-between;
}
</style>