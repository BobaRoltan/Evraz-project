<script setup>
import {ref} from "vue"
let text = ref('')
let text1 = ref('')
let tochki = ref([])
let radar = ref(0)
let blizostktochke = ref('')
let cords = ref ([])
let newTochki = ref([])

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
  tochki.value = text1.value.split(', ')
  for (let t of tochki.value) {
    let x = (1920 * t) / text.value
    newTochki.value.push(x)

  }
  tochki.value = newTochki.value

  let interval = setInterval(() => {

    let newValue = radar.value + (1920 * 10) / text.value
    let stopCoord = window.innerWidth - (1920 * 10) / text.value
    console.log(newValue, stopCoord)
    if (newValue >= stopCoord) {
      radar.value = 1900
      cords.value.push({
        x: 1900,
      })
      setTimeout(() => {
        radar.value = 0
        cords.value.push({
          x: 0,
        })
      }, 1000)
      clearInterval(interval)
    }
    else {
      radar.value = newValue
      cords.value.push({
        x: newValue,
      })
    }

    for (let tochka of newTochki.value) {
      let gap = (1920 * 10) / text.value
      let gop = (1920 * 5) / text.value
      let index = cords.value.length - 1;
      if (tochka <= radar.value + gap  && radar.value + gop <= tochka) {
        cords.value[index].left = 'Желтый свет (Дефект в пределах 10 см)'
      }
      else {
        cords.value[index].left = 'Зеленый свет (Дефектов нет)'
      }
      if (tochka >= radar.value - gap  && radar.value - gop >= tochka) {
        cords.value[index].right = 'Желтый свет (Дефект в пределах 10 см)'
      }
      else {
        cords.value[index].right = 'Зеленый свет (Дефектов нет)'
      }
    }
  }, 300)



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
  <div>Шаги проверки</div>
  <div
   v-for="(cord, index) in cords"
  >
    <div>Шаг {{index + 1}} : позиция {{ (`${ ((cord.x * text) / 1920).toFixed(0) }`) }}</div>
    <div>Левая лампа: {{ cord.right }}</div>
    <div>Правая лампа: {{ cord.left }}</div>
  </div>
</template>

<style>
.relsa {
  position: relative;
  background-color: #1D1D1D;
  margin-top: 25px;
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
  width: 10px;
  height: 16px;
  background-color: red;
}
</style>
