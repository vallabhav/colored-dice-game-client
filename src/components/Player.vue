<template>
<div  v-if="data" class="player">
  <div>
    <div class="box-top-container">
    <div class="name">
      <span v-html="data.name"></span>
    </div>
    <div class="colors" v-bind:style="{background: color}" v-for="(color) in data.colors" :key="color">
    </div>
    </div>
   <div class="player-bag">
     <PlayerBag :colors="data.colors" :bag="data.bag"/>
   </div>
  </div>
</div>
</template>

<script>
import PlayerBag from './PlayerBag.vue'
export default {
  name: 'Player',
  components: {
    PlayerBag
  },
  props: {
    data: null
  }
}
</script>
<style scoped>
div.box-top {
  margin: 5px 10px;
  height: 15px;
  width: 15px;
}

.box-top-container {
  display: flex;
  text-align: left;
  border-bottom: 2px solid darkgoldenrod;
  background-color: navajowhite;
}

.box-top-container .name {
  flex: 0 0 65%;
  margin: 15px 10px;
  font-weight: bold;
  font-size: large;
}

.box-top-container .colors {
  display: 1;
  margin: 15px 5px;
  height: 15px;
  width: 15px;
}
</style>
