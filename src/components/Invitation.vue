<template>
<div class="invitation">
    <label v-if="invitedBy">
      {{invitedBy}} has invited you to this game, please enter your name and join the game.
    </label>
    <label>
      You are invited to this game, please enter your name and join the game.
    </label><br>
    <input type="text" id="player2" name="player2" v-model="player2"><br><br>
    <button v-on:click="joinGame">Join the Game</button>
</div>
</template>

<script>
export default {
  name: 'Invitation',
  components: {
  },
  props: {
    
  },
  data () {
    return  {
      player2: '',
      gameId: String,
      invitedBy: String
    }
  },
  methods: {
    joinGame: function() {
      this.$emit('sendMessage', {name: this.player2, gameId: this.gameId, action: 'JoinGame'});
    }
  },
  created(){
      const urlParams = new URLSearchParams(window.location.search);
      this.gameId = urlParams.get('gameId');
      this.invitedBy = urlParams.get('invitedBy');
  },
}
</script>
