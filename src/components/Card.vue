<template>
  <div class="card">
    <img :src="returnImageInBase64()" />
  </div>
</template>

<script>
import tomato from '../assets/cards/tomato.png';
import cucumber from '../assets/cards/cucumber.png';
import pencil from '../assets/cards/pencil.png';
import person from '../assets/cards/person.png';
import sadboi from '../assets/cards/sadboi.png';
import sun from '../assets/cards/sun.png';
import tree from '../assets/cards/tree.png';
import xd from '../assets/cards/xd.png';

const allImages = {
  tomato,
  cucumber,
  pencil,
  person,
  sadboi,
  sun,
  tree,
  xd,
};

export default {
  name: 'Card',
  data() {
    return {
      image: '',
    };
  },
  methods: {
    returnImageInBase64() {
      return allImages[this.image];
    }
  }
}
</script>

<style scoped>
.card {
  width: 100px;
  height: 100px;
  background-color: red;
  margin: 0;
}
</style>
