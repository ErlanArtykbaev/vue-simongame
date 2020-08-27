<template>
  <div class="simon">
    <div>Simon game</div>
    <div class="game">
      <div class="buttons">
        <div class="button"></div>
        <div class="button"></div>
        <div class="button"></div>
        <div class="button"></div>
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
