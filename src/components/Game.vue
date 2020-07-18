<template>
  <div class="game-board">
    <div class="player-area" v-if="gameData">
      <div class="game-status-board">
        <label class="game-status" id="game-status" v-html="gameData.message"></label>
      </div>
      <RestartGame v-if="mode === 6" v-bind:currentPlayer="currentPlayer" v-bind:gameId="gameData.id"/>
      <ScoreBoard  v-if="mode > 4" :player1="gameData.player1.name" :player2="gameData.player2.name" 
        :player1Score="gameData.player1.score" :player2Score="gameData.player2.score" />
      <Dice v-if="mode === 5" v-bind:canRollDice="canRollDice" v-bind:currentPlayer="currentPlayer" 
      v-bind:gameId="gameData.id" v-bind:colors="gameData.colors" v-bind:computerColor="computerColor"/>
      <div class="player-panels">
        <Player :data="gameData.player1" />
        <Player :data="gameData.player2" />
        <div class="bottom"></div>
      </div>
    </div>
  </div>
</template>

<script>
import Player from './Player.vue'
import Dice from './Dice.vue'
import RestartGame from './RestartGame.vue'
import ScoreBoard from './ScoreBoard.vue'
export default {
  name: 'Game',
  components: {
    Player,
    Dice,
    RestartGame,
    ScoreBoard
  },
  props: {
    title: String,
    gameId: String,
    show: Boolean,
    gameData: null,
    id: String,
    canRollDice: Boolean,
    currentPlayer: Number,
    mode: Number,
    computerColor: String
  },
  data () {
    return  {
      
    }
  },
  methods: {
    sendDiceStatus(message) {
       this.rollDice = false
       this.updateMessage(message)
    },
    updateMessage(message) {
       this.$parent.sendMessage(message)
    }    
  }
}
</script>

<style scoped>
.player-area {
  position: relative
}
.player-panels {
  display: flex;
}
.player {
  border: 2px solid navajowhite;
  margin: 10px;
  width: 45%;
  display: 1;
}

.bottom {
  clear: both;
}

.game-status-board {
  padding: 10px;
}

.game-status {
  color: black;
}
</style>
