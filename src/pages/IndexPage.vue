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
    return alert('Напишите длину рельса')
  }
  if (isNaN(text.value) === true || Number.isInteger(+text.value) === false) {
    return alert('Напишите длину рельса целым числом')
  }
  if (text.value < 0) {
    return alert('Напишите длину рельса положительным числом')
  }
  if (text1.value===''){
    return alert('Напишите координат дефекта')
  }
  let tchki = text1.value.split(', ')
  for (let tochka of tchki) {
    if (+tochka >= +text.value || +tochka <= 0) {
      return alert('Дефект на ' + tochka + ' см не находится на рельсе')
    }
  }
  cords.value = []
  newTochki.value = []
  tochki.value = tchki


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
      radar.value = newValue // Здесь проблема
      cords.value.push({
        x: newValue,
      })
    }

    let gap = (1900 * 10) / text.value
    let gop = (1900 * 5) / text.value
    let index = cords.value.length - 1;


    let right_defect0 = newTochki.value.find(tochka => {
      return (1900 * 0) / text.value + radar.value === tochka
    })
    let right_defect1 = newTochki.value.find(tochka => {
      return (1900 * 1) / text.value + radar.value === tochka
    })
    let right_defect2 = newTochki.value.find(tochka => {
      return (1900 * 2) / text.value + radar.value === tochka
    })
    let right_defect3 = newTochki.value.find(tochka => {
      return (1900 * 3) / text.value + radar.value === tochka
    })
    let right_defect4 = newTochki.value.find(tochka => {
      return (1900 * 4) / text.value + radar.value === tochka
    })
    let right_defect5 = newTochki.value.find(tochka => {
      return (1900 * 5) / text.value + radar.value === tochka
    })
    let right_defect6 = newTochki.value.find(tochka => {
      return (1900 * 6) / text.value + radar.value === tochka
    })
    let right_defect7 = newTochki.value.find(tochka => {
      return (1900 * 7) / text.value + radar.value === tochka
    })
    let right_defect8 = newTochki.value.find(tochka => {
      return (1900 * 8) / text.value + radar.value === tochka
    })
    let right_defect9 = newTochki.value.find(tochka => {
      return (1900 * 9) / text.value + radar.value === tochka
    })
    let left_defect9 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 9) / text.value === tochka
    });
    let left_defect8 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 8) / text.value === tochka
    });
    let left_defect7 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 7) / text.value === tochka
    });
    let left_defect6 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 6) / text.value === tochka
    });
    let left_defect5 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 5) / text.value === tochka
    });
    let left_defect4 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 4) / text.value === tochka
    });
    let left_defect3 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 3) / text.value === tochka
    });
    let left_defect2 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 2) / text.value === tochka
    });
    let left_defect1 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 1) / text.value === tochka
    });
    let left_defect0 = newTochki.value.find(tochka => {
      return radar.value - (1900 * 0) / text.value === tochka
    });



    cords.value[index].right = 'Зеленый свет (Дефектов от ' + (radar.value * text.value / 1900 - 9) + ' см ' + 'до ' + (radar.value * text.value / 1900) + ' см нет)'
    cords.value[index].left = 'Зеленый свет (Дефектов от ' + (radar.value * text.value / 1900) + ' см ' + 'до ' + (radar.value * text.value / 1900 + 9) + ' см нет)'
    if(right_defect1){
      cords.value[index].left = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900 + 1) + ' см)'
    }
    else if(right_defect2){
      cords.value[index].left = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900 + 2) + ' см)'
    }
    else if(right_defect3){
      cords.value[index].left = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900 + 3) + ' см)'
    }
    else if(right_defect4){
      cords.value[index].left = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900 + 4) + ' см)'
    }
    else if(right_defect5){
      cords.value[index].left = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 + 5) + ' см)'
    }
    else if(right_defect6){
      cords.value[index].left = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 + 6) + ' см)'
    }
    else if(right_defect7){
      cords.value[index].left = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 + 7) + ' см)'
    }
    else if(right_defect8){
      cords.value[index].left = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 + 8) + ' см)'
    }
    else if(right_defect9){
      cords.value[index].left = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 + 9) + ' см)'
    }
    else if(right_defect0){
      cords.value[index].left = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900) + ' см)'
    }

    if(left_defect9){
      cords.value[index].right = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 - 9) + ' см)'
    }
    if(left_defect8){
      cords.value[index].right = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 - 8) + ' см)'
    }
    if(left_defect7){
      cords.value[index].right = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 - 7) + ' см)'
    }
    if(left_defect6){
      cords.value[index].right = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 - 6) + ' см)'
    }
    if(left_defect5){
      cords.value[index].right = 'Желтый свет (Дефект на ' + (radar.value * text.value / 1900 - 5) + ' см)'
    }
    if(left_defect4){
      cords.value[index].right = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900 - 4) + ' см)'
    }
    if(left_defect3){
      cords.value[index].right = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900 - 3) + ' см)'
    }
    if(left_defect2){
      cords.value[index].right = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900 - 2) + ' см)'
    }
    if(left_defect1){
      cords.value[index].right = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900 - 1) + ' см)'
    }
    if(left_defect0){
      cords.value[index].right = 'Красный свет (Дефект на ' + (radar.value * text.value / 1900) + ' см)'
    }
  }, 300)
}

function getColor(cord, side) {
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900) + ' см)') {
    return 'red'
  }
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900 + 1) + ' см)') {
    return 'red'
  }
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900 + 2) + ' см)') {
    return 'red'
  }
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900 + 3) + ' см)') {
    return 'red'
  }
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900 + 4) + ' см)') {
    return 'red'
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 + 5) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 + 6) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 + 7) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 + 8) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 + 9) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 - 9) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 - 8) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 - 7) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 - 6) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Желтый свет (Дефект на ' + (cord.x * text.value / 1900 - 5) + ' см)') {
    return 'yellow';
  }
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900 - 4) + ' см)') {
    return 'red'
  }
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900 - 3) + ' см)') {
    return 'red'
  }
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900 - 2) + ' см)') {
    return 'red'
  }
  if (cord[side] === 'Красный свет (Дефект на ' + (cord.x * text.value / 1900 - 1) + ' см)') {
    return 'red'
  }
    return 'green';
}
</script>

<template>
  <div class="privet">
    <p>Приветствую, посетитель. Этот сайт был создан и предназначен для нахождения дефектов на рельсе.</p>
    <p>Для начала напиши длину рельсы. Затем напишите координаты дефектов. Нажмите кнопу "Сканирование" и ожидайте.</p>
  </div>
   <div style="display: flex; align-items: center;" class="priv">
     Напишите длину рельса: <q-input  v-model="text" class="inp p"  />см

   </div>
  <div style="display: flex; align-items: center;" class="priv">
    Напишите координаты дефектов: <q-input v-model="text1" class="inp p" />см
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

    <div class="priv">Шаг {{index + 1}} : позиция {{ (`${ ((cord.x * text) / 1900).toFixed(0) }`) }} см</div>
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
