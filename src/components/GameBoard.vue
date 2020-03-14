<template>
  <main>
    <section class="gameBoard">
      <Card v-for="card in remainingCardsOnBoard"
            :key="card.key"
            :image="card.image"
            :class="[ card.class,
                    {'card--selected': selectedCards.some(c => c.class === card.class)},
                    {'card--validPair': currentValidPairImage === card.image }
                    ]"
            @click="onCardClick(card.class, card.image)" />
      <div v-if="isGameOver" class="modal">
        <div class="modal__content">
          <div class="modal__button" @click="playAgain()">Play Again</div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import Card from './Card.vue';

export default {
  name: 'GameBoard',
  components: {
    Card
  },
  data: () => ({
    cardImages: ['FeatherIcon', 'HeartIcon', 'HomeIcon', 'HeadphonesIcon', 'SunIcon', 'MoonIcon', 'ImageIcon', 'LayersIcon'],
    availableBoardCoords: ['11', '12', '13', '14', '21', '22', '23', '24', '31', '32', '33', '34', '41', '42', '43', '44'],
    cardsOnBoard: [],
    selectedCards: [],
    solvedPairs: [],
    isClickDisabled: false,
    isGameOver: false,
    currentValidPairImage: '',
    movesCounter: 0,
  }),
  mounted() {
    this.generateBoard();
  },
  updated() {
    if (this.remainingCardsOnBoard.length === 0) this.isGameOver = true;
    this.$emit('counter', this.movesCounter);
  },
  computed: {
    remainingCardsOnBoard() {
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
      if (this.selectedCards.length === 2) {
        this.movesCounter++;

        if (this.selectedCards[0].image === this.selectedCards[1].image) {
          this.isClickDisabled = true;
          setTimeout(() => { this.currentValidPairImage = image; }, 300);
          setTimeout(() => { this.solvedPairs.push(image); }, 550);
        }

        setTimeout(() => {
          this.isClickDisabled = false;
          this.clearSelection();
        }, 550);
      }
    },
    clearSelection() {
      this.selectedCards = [];
    },
    playAgain() {
      this.availableBoardCoords = ['11', '12', '13', '14', '21', '22', '23', '24', '31', '32', '33', '34', '41', '42', '43', '44'];
      this.isGameOver = false;
      this.cardsOnBoard = [];
      this.solvedPairs = [];
      this.selectedCards = [];
      this.currentValidPairImage = '';
      this.movesCounter = 0;
      this.generateBoard();
    },
    generateBoard() {
      for (let cardImagesIndex = 0; cardImagesIndex < this.cardImages.length; cardImagesIndex++) {
        for (let i = 0; i < 2; i++) {
          const coordIndex = this.getRandomInt(0, this.availableBoardCoords.length-1);

          this.cardsOnBoard.push({
            key: parseInt(`${cardImagesIndex.toString()}${i.toString()}`),
            image: this.cardImages[cardImagesIndex],
            class: `c${this.availableBoardCoords[coordIndex]}`
          });
          this.availableBoardCoords.splice(coordIndex, 1);
        }
      }
    }
  }
}
</script>

<style scoped>
.gameBoard {
  height: 436px;
  background-color: #ffb6b9;
  margin: 0 auto;
  padding: 12px;
  border: 0;
  border-radius: 7px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr;
  grid-gaps: 12px 12px;
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

.modal {
  grid-area: 1 / 1 / 5 / 5;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.modal__content {}
.modal__button {
  padding: 12px 24px;
  margin: 24px;
  font-size: 36px;
  border: 0;
  border-radius: 7px;
  background-color: #f6eec7;
  display: inline-block;
}
</style>
