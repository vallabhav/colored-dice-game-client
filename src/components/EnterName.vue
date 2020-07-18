<template>
<div class="playerName">
    <label for="player1">Enter your name</label><br>
    <input class='textbox' id="player1" type="text" name="player1" v-model="player1" placeholder="Your name"><br><br>
    <button v-on:click="newGame">Start the Game</button>
</div>
</template>

<script>
export default {
  name: 'EnterName',
  components: {
  },
  props: {
  },
  data () {
    return  {
      player1: '',
      title: '',
      msg: ''
    }
  },
  methods: {
    newGame() {
      this.msg = 'Hello ' + this.player1
      this.$emit('sendMessage', {name: this.player1, action: 'NewGame'});
    }
  }
}
</script>
<style scoped>
.playerName {
  padding: 10px;
}
</style>
