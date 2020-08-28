<template>
  <div class="simon">
    <h2>Simon game</h2>
    <div class="game">
      <div class="buttons">
        <div>
          <div class="button1 mesure"></div>
          <div class="button2 mesure"></div>
        </div>
        <div>
          <div class="button3 mesure"></div>
          <div class="button4 mesure"></div>
        </div>
      </div>
      <div class="controllers">
        <button v-on:click="start">start</button>
        <div class="round">Round: {{round}}</div>
        <div class="radio-buttons">
          <input type="radio" value="light" id="light" checked="true" v-model="complexity">
          <label for="light">Легкий</label>
          <input type="radio" value="norman" id="normal" v-model="complexity">
          <label for="normal">Нормальный</label>
          <input type="radio" value="hard" id="hard" v-model="complexity">
          <label for="hard">Сложный</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import '@/assets/styles/style.scss'

export default {
  props: ['msg'],
  data(){
    return{
      round: 1,
      complexity: ''
      }
    },
    methods: {
      start(){
        console.log('started')
      }
    }
  }
  </script>
