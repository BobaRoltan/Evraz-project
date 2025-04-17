<script setup>
import {ref} from "vue"
let text = ref('')
let text1 = ref('')
let tochki = ref([])
let radar = ref(0)

function proverka(){
  if(text.value===''){
    alert('Напишите длину рельса')
  }
  if (isNaN(text.value) === true || Number.isInteger(+text.value) === false) {
    alert('Напишите длину рельса целым числом')
  }
  if (text.value < 0) {
    alert('Напишите длину рельса положительным числом')
  }
  if (text1.value===''){
    alert('Напишите координат дефекта')
  }
  //if (isNaN(text1.value) === true) {
  //  alert('Напишите координат дефекта целым числом')
  // }
  // if (text1.value < 0) {
  //   alert('Напишите координат дефекта положительным числом')
  // }
  // if (text1.value > 10) {
  //   let tochka = text.value / 10
  //   tochki.value = tochka
  // }
  tochki.value = text1.value.split(', ')
  let newTochki = []
  for (let t of tochki.value) {
    let x = (1920 * t) / text.value
    newTochki.push(x)
  }
  tochki.value = newTochki

  let interval = setInterval(() => {
    radar.value = radar.value + (1920 * 10) / text.value
    console.log(radar.value)
  }, 1000)
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
  <div class="relsa">
    <div class="radar"
         :style="{ 'left': `${radar}px`}"
    ></div>
    <div
      v-for="defect in tochki"
      :style="{ 'left': `${ defect }px`}"
      class="defectx"
    ></div>
  </div>
</template>

<style>
.relsa {
  position: relative;
  background-color: #1D1D1D;
  width: 100%;
  height: 50px;
}
.radar{
  position: absolute;
  left: 0;
  background-color: aliceblue;
  width: 10px;
  height: 100%;
}
.defectx{
  position: absolute;
  left: 0;
  width: 16px;
  height: 16px;
  background-color: red;
}
</style>
