<script setup>
import {ref} from "vue"
let text = ref('')
let text1 = ref('')
let tochki = ref([])
let radar = ref(0)
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
  cords.value = []
  newTochki.value = []
  tochki.value = text1.value.split(', ')
  for (let t of tochki.value) {
    let x = (1900 * t) / text.value
    newTochki.value.push(x)

  }
  tochki.value = newTochki.value

  let interval = setInterval(() => {

    let newValue = radar.value + (1900 * 10) / text.value
    let stopCoord = window.innerWidth - (1900 * 9) / text.value
    console.log(newValue, stopCoord)
    if (newValue >= stopCoord) {
      // radar.value = 1900
      // cords.value.push({
      //   x: 1900,
      // })
      setTimeout(() => {
        radar.value = 0
        // cords.value.push({
        //   x: 0,
        // })
      }, 1000)
      clearInterval(interval)
    }
    else {
      radar.value = newValue
      cords.value.push({
        x: newValue,
      })
    }

    let gap = (1900 * 10) / text.value
    let gop = (1900 * 5) / text.value
    let index = cords.value.length - 1;

    let left_defect = newTochki.value.find(tochka => {
      return tochka < radar.value + gap  && radar.value < tochka;
    })

    let fulldefect = newTochki.value.find(tochka => {
      return tochka === radar.value
    })

    let right_defect = newTochki.value.find(tochka => {
      return tochka > radar.value - gap  && radar.value > tochka
    });



    cords.value[index].left = 'Зеленый свет (Дефектов нет)'
    if (left_defect) {
      cords.value[index].left = 'Желтый свет (Дефект в пределах 10 см)'
    }

    cords.value[index].right = 'Зеленый свет (Дефектов нет)'
    if (right_defect) {
      cords.value[index].right = 'Желтый свет (Дефект в пределах 10 см)'

    }
    cords.value[index].centr = 'Зеленый свет (Дефектов под радаром нет)'
    if(fulldefect){
      cords.value[index].centr = 'Красный свет(Радар стоит на девекте)'
    }
  }, 300)
}

function getColor(cord, side) {
  if (cord[side] === 'Желтый свет (Дефект в пределах 10 см)') {
    return 'yellow';
  }
  if (cord[side] === 'Красный свет(Радар стоит на девекте)') {
    return 'red'
  }
  return 'green';
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
  <div
    v-for="cord in cords"
    :style="{ left: `${ cord.x }px`}"
    style="position: absolute;"
  >
    <q-badge
      :color="getColor(cord, 'right')"
      rounded
    ></q-badge>

    <q-badge
      :color="getColor(cord, 'centr')"
      rounded
    ></q-badge>

    <q-badge
      :color="getColor(cord, 'left')"
      rounded
      ></q-badge>

  </div>

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


  <div v-if="cords.length">Шаги проверки</div>
  <div
   v-for="(cord, index) in cords"
  >
    <div>Шаг {{index + 1}} : позиция {{ (`${ ((cord.x * text) / 1900).toFixed(0) }`) }}</div>
    <div>Левая лампа: {{ cord.right }}</div>
    <div>Правая лампа: {{ cord.left }}</div>
    <div>Средняя лампа: {{cord.centr}}</div>
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
