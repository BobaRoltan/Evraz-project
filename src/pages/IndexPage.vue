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

    let right_defect1 = newTochki.value.find(tochka => {
      return tochka < radar.value + gap  && radar.value + gop < tochka;
    })

    let fulldefect = newTochki.value.find(tochka => {
      return tochka >= radar.value && radar.value + gop > tochka;
    })

    let left_defect = newTochki.value.find(tochka => {
      return tochka > radar.value - gap  && radar.value - gop > tochka
    });



    cords.value[index].left = 'Зеленый свет (Дефектов нет)'
    if (right_defect1) {
      cords.value[index].left = 'Желтый свет (Дефект в пределах 5-10 см)'
    }


    cords.value[index].right = 'Зеленый свет (Дефектов нет)'
    if (left_defect) {
      cords.value[index].right = 'Желтый свет (Дефект в пределах 5-10 см)'

    }
    cords.value[index].centr = 'Зеленый свет (Дефектов под радаром нет)'
    if(fulldefect){
      cords.value[index].left = 'Красный свет (Дефект в пределах 0-5 см)'
    }
  }, 300)
}

function getColor(cord, side) {
  if (cord[side] === 'Желтый свет (Дефект в пределах 5-10 см)') {
    return 'yellow';
  }
  if (cord[side] === 'Красный свет (Дефект в пределах 0-5 см)') {
    return 'red'
  }
  return 'green';
}
</script>

<template>
  <div class="privet">
    <p>Приветствую, посетитель. Этот сайт был создан и предназначен для нахождения дефектов на рельсе.</p>
    <p>Для начала напиши длину рельсы. Затем напишите координату дефекта. Нажмите кнопу "Сканирование" и ожидайте.</p>
  </div>
   <div style="display: flex; align-items: center;" class="priv">
     Напишите длину рельса: <q-input  v-model="text" class="inp p"  />см

   </div>
  <div style="display: flex; align-items: center;" class="priv">
    Напишите координат дефекта: <q-input v-model="text1" class="inp p" />см
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


  <div class="priv" v-if="cords.length">Шаги проверки</div>
  <div class="priv" v-if="cords.length">Общее количество шагов: {{cords.length}}</div>
  <div
   v-for="(cord, index) in cords"
  >

    <div class="priv">Шаг {{index + 1}} : позиция {{ (`${ ((cord.x * text) / 1900).toFixed(0) }`) }}</div>
    <div class="priv">Левая лампа: {{ cord.right }}</div>
    <div class="priv">Правая лампа: {{ cord.left }}</div>
  </div>
</template>

<style>
.p{
  font-size : 18px;
}
.priv{
  font-size : 20px;
}
.privet{
  font-size : 18px;
}
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
