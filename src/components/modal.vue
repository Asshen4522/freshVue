<script setup>
const emit = defineEmits([
    'modalYes','modalNo'
])
const props = defineProps({
    modalType: "",
    modalText: ""
})
</script>
<template>
    <div class="container">
        <div class="modal-back"></div>
        <div class="modal-main">
            <div class="header">
                {{ props.modalText }}
            </div>
            <div v-if="props.modalType=='answer'">
                <button @click="$emit('modalYes')">Да</button>
                <button @click="$emit('modalNo')">Нет</button>
            </div>
            <div v-else><button @click="$emit('modalYes')">Понял</button></div>
        </div>
    </div>
   
</template>
<style scoped>
.modal-back{
    position: fixed;
    top: 0;
    left: 0;
    min-width: 100vw;
    min-height: 100vh;
    z-index: 999;

    
    background-color: grey;
    opacity: 0.5;
    
}
.modal-main{
    background-color: white;
    width: 300px;
    height: 300px;
    z-index: 1000;

    display: flex;
    flex-direction: column;
    padding: 40px;
    align-items: center;
}
.container{
    position: fixed;
    top: 0;
    left: 0;
    
    min-width: 100vw;
    min-height: 100vh;

    display: flex;
    align-items: center;
    justify-content: center;
}
.header{
    margin-top: 50px;
    margin-bottom: 100px;
}
</style>