<template>
  <div id="app">
    <Game v-bind:msg="msg" />
  </div>
</template>

<script>
import Game from './components/Game'

export default {
  name: 'App',
  components: {
    Game
  },
  data(){
    return{
      msg: 'hello world'
    }
  }
}
</script>

<style lang="sass">
#app 
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px

</style>
