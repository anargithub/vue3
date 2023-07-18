<template>
  <div>
    
    <textarea v-model="newBlock"></textarea>
    <button @click="addBlock">Добавить блок</button>
    <div 
      v-for="(block, id) in blocks" 
      :key="id" 
      :class="'blockSelected'" 
      :style="getBlockStyles(id)">

        {{ block }}

        <br>
        Цвет текста
        <select v-model="blockStyles[id].color"> 
          <option value="red">Красный</option>
          <option value="blue">Синий</option>
          <option value="green">Зеленый</option>
        </select><br>
        Фон
        <select v-model="blockStyles[id].background">
          <option value="yellow">Желтый</option>
          <option value="pink">Розовый</option>
          <option value="teal">Зеленый</option>
        </select><br>
        Шрифт
        <select v-model="blockStyles[id].fontFamily">
        <option value="Arial">Arial</option>
        <option value="Times New Roman">Times New Roman</option>
        <option value="Verdana">Verdana</option>
        </select><br>
        Размер шрифта
        <input type="number" v-model="blockStyles[id].fontSize" min="10" max="48" step="2"> px <br>
        <label>
          <input type="checkbox" v-model="blockStyles[id].italic"> Курсив
        </label>
        <label>
          <input type="checkbox" v-model="blockStyles[id].bold"> Жирный
        </label>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const blocks = ref([])
const newBlock = ref('')
const blockStyles = ref([])


const addBlock = () => {
  blocks.value.push(newBlock.value)
  blockStyles.value.push({
    color: 'black',
    background: 'white',
    fontFamily: 'Arial',
    fontSize: 14,
    italic: false,
    bold: false
  })
}
const getBlockStyles = (id) => {
  const style = blockStyles.value[id]
  return {
    color: style.color,
    background: style.background,
    fontFamily: style.fontFamily,
    fontSize: style.fontSize + 'px',
    fontStyle: style.italic ? 'italic' : 'normal',
    fontWeight: style.bold ? 'bold' : 'normal'
  }
}
</script>

<style scoped>

</style>