<template>
  <div id="app">
    <ColorDiceGame :msg="msg"/>
  </div>
</template>

<script>
import ColorDiceGame from './components/ColorDiceGame.vue'

export default {
  name: 'App',
  components: {
    ColorDiceGame
  },
  data () {
    return  {
      msg: "Hello"
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #776e65;
  background: #faf8ef;
  width: 70%;
  margin: 0 auto;
}
</style>
