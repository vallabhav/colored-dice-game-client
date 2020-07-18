<template>
  <div id="color-dice-game">
    <!--<h1>{{ msg }}</h1>
    <h3>{{mode}}</h3>-->
    <div class="game-title">{{ title }}</div>
    <EnterName v-if="mode === 1" :msg="msg" :title="title" v-on:sendMessage="sendMessage"/>
    <invitation v-if="mode === 3" v-on:sendMessage="sendMessage"/>
    <ChooseSecondPlayer v-if="mode === 4" v-bind:gameId="gameId" v-bind:inviteUrl="inviteUrl"/>
    <Game  v-if="mode > 3" v-bind:inviteUrl="inviteUrl" v-bind:mode="mode"
       v-bind:currentPlayer="playerId" :title="title" v-bind:gameData="dataObj" v-bind:id="gameId" 
       v-bind:computerColor="computerColor" v-bind:canRollDice="canRollDice"/>
  </div>
</template>

<script>
const Mode = Object.freeze({"IniateGame" : 1, "StartGame":2, "GameInvite":3,"GameIniated": 4, "GameStarted":5, "GameOver":6})
const GameStatus = Object.freeze({'Iniated': 'iniated', 'Ready': 'ready', 'Inprogress': 'inprogress', 'Over' : 'over' })
import Socket from "./socket"
import EnterName from './EnterName.vue'
import Invitation from './Invitation.vue'
import ChooseSecondPlayer from './ChooseSecondPlayer.vue'
import Game from './Game.vue'
import emitter from './socket'

export default {
  name: 'ColorDiceGame',
  components: {
    EnterName,
    Invitation,
    ChooseSecondPlayer,
    Game
  },
  
  data () {
    return  {
      msg: "Hello",
      title: "Game Board",
      connection: null,
      dataObj: {
        type: Object,
        default: () => ({})
      },
      gameId: null,
      inviteUrl: '',
      mode: Mode.IniateGame,
      playerId: null,
      canRollDice: false,
      computerColor: ''
    }
  }, 
  methods: {
      handleMessage(msg) {
        this.dataObj = JSON.parse(msg)
        this.gameId = this.dataObj.id
        if (this.dataObj.status === GameStatus.Iniated) {
          this.inviteUrl = this.addQueryParam('gameId=' + this.dataObj.id)
          this.inviteUrl = this.addQueryParam('invitedBy=' +  this.dataObj.player1.name, this.inviteUrl)
          this.mode = Mode.GameIniated
          this.playerId = this.dataObj.player1.id;
        } else if (this.dataObj.status === GameStatus.Ready) {
          if (this.mode === Mode.GameInvite) {
            this.playerId = this.dataObj.player2.id;
          }
          this.mode = Mode.GameStarted
          if (this.playerId === this.dataObj.currentPlayer) {
            this.canRollDice = true
          }
        } else if (this.dataObj.status === GameStatus.Inprogress) {
          if (this.playerId === this.dataObj.currentPlayer) {
            this.canRollDice = true
          } else {
            this.canRollDice = false
            // handle computer's play
            if (this.dataObj.player2.isComputer && this.dataObj.currentPlayer === this.dataObj.player2.id) {
                this.computerColor  = this.getRandomColor(this.dataObj.colors)
                this.sendMessage({playerId: this.dataObj.currentPlayer, gameId: this.gameId, color: this.computerColor, action: 'RollDice'});
            }
          }
        } else if (this.dataObj.status === GameStatus.Over) {
          this.mode = Mode.GameOver
          this.canRollDice = false
        }
      },

      sendMessage(message) {
        if (message.action === 'NewGame' || message.action === 'JoinGame') {
          this.msg = 'Hello ' + message.name;
        } else if(message.action ==='RollDice') {
          this.canRollDice = false;
        }
        emitter.send(JSON.stringify(message));
      },
      addQueryParam(param, url) {
        let _url = url ? url :window.location.href
        _url += (_url.split('?')[1] ? '&':'?') + param
        return _url
      },
      getRandomColor(colors) {
        return colors[Math.floor(Math.random() * colors.length)];
      }
  },
  created(){
      Socket.$on("message", this.handleMessage)
      const urlParams = new URLSearchParams(window.location.search);
      const myParam = urlParams.get('gameId');
      if (myParam) {
        this.mode = Mode.GameInvite
      }
  },
  beforeDestroy(){
      Socket.$off("message", this.handleMessage)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#color-dice-game {
  border: 2px solid navajowhite;
  padding: 0px 0px 20px 0px;
}
.game-title {
  background: navajowhite;
  font-weight: bold;
  font-size: x-large;
  padding: 10px;
  font-family: cursive;
}
</style>
