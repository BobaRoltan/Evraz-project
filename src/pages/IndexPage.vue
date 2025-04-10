<script setup>
import {ref} from "vue"
let text = ref('')
let text1 = ref('')
function proverka(){
  if(text.value===''){
    alert('Напишите длину рельса')
  }
  if (isNaN(text.value) === true) {
    alert('Напишите длину рельса числом')
  }
  if (text.value < 0) {
    alert('Напишите длину рельса правильно')
  }
  if (text1.value===''){
    alert('Напишите координат дефекта')
  }
  if (isNaN(text1.value) === true) {
    alert('Напишите координат дефекта числом')
  }
  if (text1.value < 0) {
    alert('Напишите координат дефекта правильно')
  }
}
</script>

<template>
   <div style="display: flex; align-items: center;">
     Напишите длину рельса: <q-input  v-model="text" class="inp" />см

   </div>
  <div style="display: flex; align-items: center;">
    Напишите координат дефекта: <q-input v-model="text1" class="inp" />см
  </div>
  <q-btn color="orange" label="Сканирование" @click="proverka"></q-btn>
</template>

<style>
</style>
