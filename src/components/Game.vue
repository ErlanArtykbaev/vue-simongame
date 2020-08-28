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
          <input type="radio" value="normal" id="normal" v-model="complexity">
          <label for="normal">Нормальный</label>
          <input type="radio" value="hard" id="hard" v-model="complexity">
          <label for="hard">Сложный</label>
        </div>
      </div>
    </div>
    <audio ref="muz1" src="../assets/mp3/1.ogg"></audio>
    <audio ref="muz2" src="../assets/mp3/2.ogg"></audio>
    <audio ref="muz3" src="../assets/mp3/3.ogg"></audio>
    <audio ref="muz4" src="../assets/mp3/4.ogg"></audio>
  </div>
</template>

<script>
import '@/assets/styles/style.scss'

const delay = delayed => (
  new Promise(resolve => setTimeout(resolve, delayed))
)

export default {
  data(){
    return{
      secondsInterval: 0,
      round: 1,
      complexity: 'light',
      sequence: [],
      canClick: false,
      sequenceToGuess: []
    }
  },
  methods: {
    async start(){
      this.canClick = false
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
        await delay(this.secondsInterval)
        console.log(el)
      }
      this.sequenceToGuess = [...this.sequence]
      this.canClick = true
    },

    async clicked(e){
      if(!this.canClick) return
      e.target.classList.toggle('active')
      this.playMusic(e.target)
      await delay(300)
      e.target.classList.toggle('active')

      let expectedPanel = this.sequenceToGuess.shift()
      if(expectedPanel === e.target){
        if(this.sequenceToGuess.length === 0){
          await delay(1000)
          //start new round
          this.round++
          this.start()
          this.sequenceToGuess = [...this.sequence]
        }
      }else{
        alert('game is over')
        this.round = 1
        this.sequence = []
      }
    },

    flash(panel){
      return new Promise((resolve, reject) => {
        this.playMusic(panel)
        setTimeout(() => {
          panel.classList.toggle('active')
        }, this.secondsInterval)
        setTimeout(() => {
          resolve()
        }, 200);
      })
      .then(() => {
        panel.classList.toggle('active')
      })
    },
    
    sequencePush(){
      this.sequence.push(this.getRandomPanel())
    },

    getRandomPanel(){
      const panels = [
        this.$refs.button1,
        this.$refs.button2,
        this.$refs.button3,
        this.$refs.button4
      ]
      return panels[parseInt(Math.random() * panels.length)]
    },

    playMusic(panel){
      switch(panel){
        case this.$refs.button1:
          this.$refs.muz1.play()
          break
        case this.$refs.button2:
          this.$refs.muz2.play()
          break
        case this.$refs.button3:
          this.$refs.muz3.play()
          break
        case this.$refs.button4:
          this.$refs.muz4.play()
          break
      }
    }
  }
}
</script>
