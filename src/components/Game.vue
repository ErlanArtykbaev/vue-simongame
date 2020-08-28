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
      <div class="controlers">
        <button v-on:click="start">start</button>
        <input type="radio" name="light" id="light">
        <input type="radio" name="norman" id="normal">
        <input type="radio" name="hard" id="hard">
      </div>
    </div>
  </div>
</template>

<script>
import '@/assets/styles/style.scss'

export default {
  props: ['msg'],
  methods: {
    start(){
      console.log('started')
    }
  }
}
</script>
