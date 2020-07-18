<template>
<div class="score-board">
  <span class="player" v-html="player1"></span> : <span class="score" v-html="player1Score"></span><br>
  <span class="player" v-html="player2"></span> : <span  class="score" v-html="player2Score"></span>
</div>
</template>

<script>
export default {
  name: 'ScoreBoard',
  components: {
  },
  props: {
    player1: String,
    player1Score: Number,
    player2: String,
    player2Score: Number
  }
}
</script>
<style scoped>
.score-board {
  position:absolute;
  top:0;
  right:0;
  padding: 5px;
  border-left: 2px solid navajowhite;
  border-bottom: 2px solid navajowhite;
  font-size: 12px
}

.score-board .player {
  float: left;
}

.score-board .score {
  font-weight: bold;
  color: black;
  float: right;
}
</style>
