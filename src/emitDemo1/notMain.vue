<script setup>
const emit = defineEmits([
  'actionOne'
])

function fun() {
  emit('actionOne','Строка из компонента')
}
</script>
<template>
  <button @click="fun">Нажать</button>
</template>
<style scoped>
</style>