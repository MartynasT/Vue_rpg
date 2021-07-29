<template>
  <div id="app">
    <div class="arena">
      <!--    user-->
      <Player :info="player" />
      <div class="game-logic">
        <!--    gold-->
        <h2> 💰: {{player.gold}}</h2>
        <!--    button-->
        <button @click="attack" >Attack</button>
        <!--    potion-->
        <div class="potion">
          <img :src="potion.img" alt="">
          <h3>Price: 50 💰</h3>
          <button @click="buyPotion">Buy</button>
        </div>
      </div>

      <!--    enemy-->
      <Player :info="enemies[currentEnemy]" />
    </div>
    <!--    weapons-->
    <div class="weapons">
      <Weapon v-for="(item, i) in weapons" :key="i" :item="item"/>
    </div>



  </div>
</template>

<script>
import Player from '@/components/Player'
import Weapon from '@/components/Weapon'

export default {
  name: 'App',
  components: {
    Player,
    Weapon
  },
  data(){
    return{
      player: {
        name: 'player',
        health: 100,
        gold: 0,
        img: 'https://i.pinimg.com/originals/99/a7/9e/99a79e297d9502e5973e86450ae7134b.jpg',
        damage: 10,
      },
      enemies: [
        {
          name: "Goblin",
          img: "https://i.imgur.com/yBh7Fn4.png",
          maxDamage: 12,
          health: 100,
        },
        {
          name: "Troll",
          img: "https://i.pinimg.com/originals/8d/7f/d8/8d7fd8ae9fcd6060497c628e1c7944b4.jpg",
          maxDamage: 8,
          health: 100,
        },
        {
          name: "Witch",
          img: "https://i.pinimg.com/originals/c0/da/c0/c0dac0da46b4c59534cf898b1967d523.png",
          maxDamage: 15,
          health: 100,
        }
      ],
      weapons: [
        {
          name: 'sword',
          img: "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRjeRzenAFh9nuqc0sexfw63azpjKmulkubHg&usqp=CAU",
          damage: 10,
          effect: 'gives player 25% chance to doge enemy attacks'
        },
        {
          name: 'magicWand',
          img: "https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRYLtdkk7fwbEwdjNpuL0Oo1ka5A7z0PhL34Q&usqp=CAU",
          damage: 12,
          effect: 'heals player on every enemy hit from 0 to 5 hit points'
        },
        {
          name: 'bow',
          img: "https://preview.pixlr.com/images/800wm/100/1/1001468630.jpg",
          damage: 7,
          effect: 'has a 50% chance to hit enemy two times in a row'
        },
      ],
      potion: {
        img: "https://preview.pixlr.com/images/450nwm/100/1/1001468594.jpg",
            info: "can be bought from shop for 50 coins, recovers player health when bought",
      },
      currentEnemy: 0
    }
  },
  methods:{
    giveGold(){
      this.player.gold +=  (Math.floor(Math.random() * 10));
    },
    attack(){
      // const userAttack =
      console.log(Math.floor(Math.random()* this.enemies.length ))
      const userAttack = () => Math.floor(Math.random()*(this.player.damage +1));
      const enemyAttack = () => Math.floor(Math.random()*(this.enemies[this.currentEnemy].maxDamage +1));

      this.player.health -= enemyAttack();
      this.enemies[this.currentEnemy].health -= userAttack()

      if (this.enemies[this.currentEnemy].health <= 0){
        this.enemies[this.currentEnemy].health = 100;
        this.currentEnemy = Math.floor(Math.random()* this.enemies.length )
      }

      this.giveGold()
    },
    buyPotion(){
      const {player} = this
      if (player.gold >= 50){
        player.gold -= 50
        player.health = 100
      }
    }

  },
  mounted () {
    //set first Enemy
    this.currentEnemy = Math.floor(Math.random()* this.enemies.length )
  }
}
</script>

<style>
.arena{
  display: flex;
  justify-content: space-between;
}

.potion{
  width: 200px;
}

.potion img{
  width: 100%;
}

.weapons{
  display: flex;
}

</style>

<!--// create a game where player fights against monster-->
<!--// player and monster should both have health bars representing health left-->
<!--// 100 health points each-->
<!--// game goes like this: player clicks button "hit" and hits enemy-->
<!--// then enemy automatically hits player back with random damage from 0 to max damage it makes-->
<!--// when enemy is killed, second random enemy appear with full health bar-->


<!--// player should be able to change weapon he is equipped with-->
<!--// each weapon will have it's own effect on player-->
<!--// (player should have 3 weapons to choose, but can hold only one while fighting)-->
<!--// on every hit player gets random amount of coins - from 0 to 10-->
<!--// coins are needed to buy health potions, one potion costs 50 points-->
<!--// health potions fully restores player health when bought-->





