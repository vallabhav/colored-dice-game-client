<template>
  <div class="color-bag">
    <div v-for="(color) in colors" :key="color" class="color-bag-row">
       <div :key="index" v-bind:style="{background: color}" class="bag" v-for="(index) in bag[color]"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PlayerBag',
  props: {
    colors: Array,
    bag: null
  }
}
</script>
<style>
.color-bag-row {
  display: flex;
}
.color-bag-row .bag {
  display: 1;
  margin: 15px 10px;
  height: 50px;
  width: 50px;
}
</style>
