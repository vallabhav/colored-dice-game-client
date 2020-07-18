<template>
<div class="restart-game">
  <button v-on:click="playAgain">Play again</button>
  <br>
</div>
</template>

<script>
export default {
  name: 'RestartGame',
  components: {
  },
  props: {
    gameId: String,
    currentPlayer: Number,
  },
  methods: {
    playAgain() {
      this.$parent.updateMessage({gameId: this.gameId, playerId: this.currentPlayer, action: 'PlayAgain'});
    }
  }
}
</script>
