<template>
  <div class="weapon">
    <img :src="item.img" alt="">
    <h3>{{item.name}}</h3>
    <h3>{{item.damage}}</h3>
    <h4>{{item.effect}}</h4>
  </div>
</template>

<script>
export default {
  name: 'Weapon',
  props: ['item']
}
</script>

<style scoped>
  .weapon{
    text-align: center;
  }
  .weapon img{
    width: 100px;
  }
</style>