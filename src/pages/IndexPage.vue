<script setup>
import {ref} from "vue"
let text = ref('')
let text1 = ref('')
let tochki = ref([])
function proverka(){
  if(text.value===''){
    alert('Напишите длину рельса')
  }
  if (isNaN(text.value) === true || Number.isInteger(+text.value) === false) {
    alert('Напишите длину рельса целым числом')
  }
  console.log(Number.isInteger(+text.value))
  if (text.value < 0) {
    alert('Напишите длину рельса положительным числом')
  }
  if (text1.value===''){
    alert('Напишите координат дефекта')
  }
  if (isNaN(text1.value) === true) {
    alert('Напишите координат дефекта целым числом')
  }
  if (text1.value < 0) {
    alert('Напишите координат дефекта положительным числом')
  }
  if (text1.value > 10) {
    let tochka = text.value / 10
    tochki.value = tochka
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
  <div class="radar"></div>
  <div class="relsa"></div>
</template>

<style>
.relsa{
  background-color: #1D1D1D;
  margin-top: 50px;
  padding-bottom: 10px;
  padding-top: 10px;
}
.radar{
  background-color: black;
  padding-bottom: 5px;
  padding-top: 5px;
  border-right: 100px;
}
</style>
