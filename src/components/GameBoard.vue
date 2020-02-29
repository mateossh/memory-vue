<template>
  <section class="gameBoard">
    <Card v-for="card in activeCards"
          :key="card.key"
          :image="card.image"
          :imageBase64="cardImages[card.image]"
          :class="[ card.class,
                  {'card--selected': selectedCards.some(c => c.class === card.class)},
                  {'card--validPair': currentValidPairImage === card.image }
                  ]"
          @click="onCardClick(card.class, card.image)" />
  </section>
</template>

<script>
import Card from './Card.vue';
import tomato from '../assets/cards/tomato.png';
import cucumber from '../assets/cards/cucumber.png';
import pencil from '../assets/cards/pencil.png';
import person from '../assets/cards/person.png';
import sadboi from '../assets/cards/sadboi.png';
import sun from '../assets/cards/sun.png';
import tree from '../assets/cards/tree.png';
import xd from '../assets/cards/xd.png';

const availableBoardCoords = ['11', '12', '13', '14', '21', '22', '23', '24', '31', '32', '33', '34', '41', '42', '43', '44'];

export default {
  name: 'GameBoard',
  components: {
    Card
  },
  data: () => ({
    cardImages: {
      tomato,
      cucumber,
      pencil,
      person,
      sadboi,
      sun,
      tree,
      xd,
    },
    cardsOnBoard: [],
    selectedCards: [],
    solvedPairs: [],
    isClickDisabled: false,
    currentValidPairImage: '',
  }),
  mounted() {
    this.generateBoard();
  },
  computed: {
    activeCards() {
      return this.cardsOnBoard.filter(card => !this.solvedPairs.includes(card.image));
    },
  },
  methods: {
    getRandomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    onCardClick(className, image) {
      if (this.selectedCards.length < 2 && !this.isClickDisabled) {
        // NOTE: De Morgan's law -> this.selectedCards.length == 1 && this.selectedCards[0].class === className
        if (this.selectedCards.length != 1 || this.selectedCards[0].class !== className) {
          this.selectedCards.push({ class: className, image });
        }
      }

      if (!this.isClickDisabled) this.handleCardsMatching(className, image);
    },
    handleCardsMatching(className, image) {
      if (this.selectedCards[0].image === this.selectedCards[1].image) {
        this.isClickDisabled = true;
        setTimeout(() => { this.currentValidPairImage = image }, 300 );
        setTimeout(() => {
          this.isClickDisabled = false;
          this.solvedPairs.push(image);
          this.clearSelection();
        }, 550);
      }
      if (this.selectedCards.length === 2) {
        setTimeout(() => {
          this.isClickDisabled = false;
          this.clearSelection();
        }, 550);
      }
    },
    clearSelection() {
      this.selectedCards = [];
    },
    generateBoard() {
      const possibleCards = Object.keys(this.cardImages);

      for (let i = 0; i < possibleCards.length; i++) {
        for (let j = 0; j < 2; j++) {
          const index = this.getRandomInt(0, availableBoardCoords.length-1);

          this.cardsOnBoard.push({
            key: parseInt(`${i.toString()}${j.toString()}`),
            image: possibleCards[i],
            class: `c${availableBoardCoords[index]}`
          });
          availableBoardCoords.splice(index, 1);
        }
      }
    }
  }
}
</script>

<style scoped>
.gameBoard {
  width: 460px;
  height: 460px;
  background-color: #ffb6b9;
  margin: 0 auto;
  padding: 6px;
  border: 0;
  border-radius: 7px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr;
  perspective: 6000px;
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
