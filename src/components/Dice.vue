<template>
<div class="dice-section">
<div class="dice">
  <div class="dot" v-bind:style="{background: color}"></div>
</div>
 <button :disabled="canRollDice === false"  v-on:click="rollDice">Roll Dice</button>
</div>
</template>

<script>
export default {
  name: 'Dice',
  components: {
  },
  props: {
    canRollDice: Boolean,
    currentPlayer: Number,
    gameId: String,
    colors: Array,
    computerColor: String
  },
  data () {
    return  {
      color: '',
      colorBefore: ''
    }
  },
  methods: {
    rollDice() {
       this.color = this.colors[Math.floor(Math.random() * this.colors.length)];
       this.$parent.sendDiceStatus({playerId: this.currentPlayer, gameId: this.gameId, color: this.color, action: 'RollDice'});
    }
  },
  created(){
    // to do
  },
  watch: { 
      computerColor: function(newVal, oldVal) { // watch it
        this.colorBefore = oldVal
        this.color = newVal
      }
  }
}
</script>
<style scoped>
.dice-selection {
    width: 30%;
    margin: 0 35%;
    padding: 5px;
}
.dice {
  border: 3px solid navajowhite;
  height: 50px;
  width: 50px;
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  margin: 5px 0;
  background: mintcream;
}

.dot {
    align-self: center;
    border-radius: 50%;
    display: block;
    height: 1.50rem;
    justify-self: center;
    width: 1.50rem;
    position: absolute;
    top: 14px;
    left: 14px;
}

</style>
