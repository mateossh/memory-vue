<template>
  <div class="gameBoard">
    <Card class="c11"/>
    <Card class="c12"/>
    <Card class="c13"/>
    <Card class="c14"/>

    <Card class="c21"/>
    <Card class="c22"/>
    <Card class="c23"/>
    <Card class="c24"/>

    <Card class="c31"/>
    <Card class="c32"/>
    <Card class="c33"/>
    <Card class="c34"/>

    <Card class="c41"/>
    <Card class="c42"/>
    <Card class="c43"/>
    <Card class="c44"/>

  </div>
</template>

<script>
import Card from './Card.vue';

const possibleCards = ['tomato', 'cucumber', 'pencil', 'person', 
                       'sadboi', 'sun', 'tree', 'xd'];
let retriesCounter = 0;

export default {
  name: 'GameBoard',
  components: {
    Card
  },
  mounted() {
    console.log('mounted ;)');

    this.generateBoard(); // TODO: invent better board generator
  },
  methods: {
    getRandomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    generateBoard() {
      for (let i = 0; i < possibleCards.length; i++) {
        const first = this.getRandomInt(0, 15);
        const second = this.getRandomInt(0, 15);
        console.log('XXXX', possibleCards[i], first+1, second+1, this.$children[first].image, this.$children[second].image);

        if (first === second) {
          console.log('first === second !!!! restarting loop');
          i--;
          retriesCounter++;
          continue;
        }

        if (this.$children[first].image !== '' || this.$children[second].image !== '') {
          console.log('first === second !!!! restarting loop');
          i--;
          retriesCounter++;
          continue;
        }

        if (this.$children[first].image === '' && this.$children[second].image === '') {
          this.$children[first].image = possibleCards[i];
          this.$children[second].image = possibleCards[i];
        }
      }
      console.log('XXXX: generating finished retriesCounter', retriesCounter);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.gameBoard {
  width: 400px;
  height: 400px;
  margin: 0 auto;
  border: 1px solid black;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr;
}

.c11 { grid-area: 1 / 1 / 1 / 1; }
.c12 { grid-area: 1 / 2 / 1 / 2; }
.c13 { grid-area: 1 / 3 / 1 / 3; }
.c14 { grid-area: 1 / 4 / 1 / 4; }

.c21 { grid-area: 2 / 1 / 2 / 1; }
.c22 { grid-area: 2 / 2 / 2 / 2; }
.c23 { grid-area: 2 / 3 / 2 / 3; }
.c24 { grid-area: 2 / 4 / 2 / 4; }

.c31 { grid-area: 3 / 1 / 3 / 1; }
.c32 { grid-area: 3 / 2 / 3 / 2; }
.c33 { grid-area: 3 / 3 / 3 / 3; }
.c34 { grid-area: 3 / 4 / 3 / 4; }

.c41 { grid-area: 4 / 1 / 4 / 1; }
.c42 { grid-area: 4 / 2 / 4 / 2; }
.c43 { grid-area: 4 / 3 / 4 / 3; }
.c44 { grid-area: 4 / 4 / 4 / 4; }

</style>
