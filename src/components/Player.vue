<template>
  <div class="player">
    <img :src="info.img" alt="">
    <div class="hp-holder" >
      <div class="hp" :style="{ width: info.health+ '%' } ">
        {{info.health}}
      </div>
    </div>
    <h2>{{info.name}}</h2>
  </div>
</template>

<script>
export default {
  name: 'Player',
  props: ['info']
}
</script>

<style scoped>
  .player img{
    width: 300px;
  }

  .hp-holder {
    width: 300px;
    height: 20px;
  }
  .hp{
    height: 20px;
    background-color: #1b9d7f;
  }
</style>