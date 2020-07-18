<template>
<div class="choose-second-player">
  <br>
  <label>Copy the following link and share it with your friend, so that he/she can join the game.</label><br>
  <label class="invite-url" v-html="inviteUrl"></label>
  <br><br>
  <span>( Or )</span>
  <br><br>
  <button v-on:click="chooseComputer">Play with computer</button>
  <br><br>
</div>
</template>

<script>
export default {
  name: 'ChooseSecondPlayer',
  components: {
  },
  props: {
    gameId: String,
    inviteUrl: String
  },
  methods: {
    chooseComputer() {
      this.$parent.sendMessage({name: 'computer', isComputer: true, gameId: this.gameId, action: 'JoinGame'});
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.textbox {
  font-size: 18px;
  padding: 8px 10px !important;
  width: 172px;
  border-color: #bdc7d8;
  border-radius: 5px;
  margin: 0;
  border: 1px solid #ccd0d5
}

.invite-url {
  color: blue
}

</style>
