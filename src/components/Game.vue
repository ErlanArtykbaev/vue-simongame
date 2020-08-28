<template>
  <div class="simon">
    <h2>Simon game</h2>
    <div class="game">
      <div class="buttons">
        <div>
          <div 
            class="button1 mesure" 
            @click="clicked"></div>
          <div 
            class="button2 mesure" 
            @click="clicked"></div>
        </div>
        <div>
          <div 
            class="button3 mesure" 
            @click="clicked"></div>
          <div 
            class="button4 mesure" 
            @click="clicked"></div>
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
  data(){
    return{
      secondsInterval: 0,
      round: 1,
      complexity: 'light'
      }
    },
    methods: {
      start(){
        switch(this.complexity){
          case 'light':
            this.secondsInterval = 1500
            break
          case 'normal':
            this.secondsInterval = 1000
            break
          case 'hard':
            this.secondsInterval = 300
            break
        }
        console.log('started')
      },
      clicked(e){
        e.target.classList.toggle('active')
      }
    }
  }
  </script>
