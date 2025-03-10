<script setup>
const props = defineProps({
    text : String
})

const emit = defineEmits([
    'closeModal'
])

function fun() {
    emit('closeModal') 
}


</script>
<template>
    <div class="container">
        <div class="modal-main">
            {{ props.text }}
            <button @click="fun">Сгинь, окно</button>
        </div>
        <div class="modal-back">
        </div>
    </div>
</template>
<style scoped>
.container{
    position: fixed;
    top: 0;
    left: 0;

    min-height: 100vh;
    min-width: 100vw;

    display: flex;
    align-items: center;
    justify-content: center;
}

.modal-main{
    width: 400px;
    height: 400px;
    z-index: 1000;
    background-color: aqua;
}
.modal-back{
    position: fixed;
    top: 0;
    left: 0;

    min-height: 100vh;
    min-width: 100vw;

    z-index: 999;
    background-color: grey;
    opacity: 0.5;
}
</style>