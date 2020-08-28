<template>
  <div class="simon">
    <h2>Simon game</h2>
    <div class="game">
      <div class="buttons">
        <div>
          <div 
            ref="button1"
            class="button1 mesure" 
            @click="clicked"></div>
          <div 
            class="button2 mesure" 
            ref="button2"
            @click="clicked"></div>
        </div>
        <div>
          <div 
            class="button3 mesure" 
            ref="button3"
            @click="clicked"></div>
          <div 
            class="button4 mesure" 
            ref="button4"
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
      complexity: 'light',
      sequence: [],
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
      this.sequencePush()
      for(const el of this.sequence){
        this.flash(el)
      }
    },
    clicked(e){
      e.target.classList.toggle('active')
      setTimeout(() => {
        e.target.classList.toggle('active')
      }, 200);
    },
    flash(panel){
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          panel.classList.toggle('active')
        }, this.secondsInterval)
        resolve()
      })
      .then(() => {
        panel.classList.toggle('active')
      })
    },
    sequencePush(){
      this.sequence.push(this.$refs.button1)
      this.sequence.push(this.$refs.button2)
      this.sequence.push(this.$refs.button3)
      this.sequence.push(this.$refs.button4)
    }
  }
}
</script>
