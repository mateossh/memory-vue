<template>
  <div class="card" @click="$emit('click')">
    <div class="card__face card__face--front"></div>
    <div class="card__face card__face--back">
      <img :src="imageBase64" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    imageBase64: String,
  },
}
</script>

<style scoped>
@keyframes disappear {
  from { opacity: 1; }
  to { opacity: 0; }
}
@-webkit-keyframes disappear {
  from { opacity: 1; }
  to { opacity: 0; }
}
.card {
  width: 100px;
  height: 100px;
  background-color: #f6eec7;
  place-self: center; /* align-self / justify-self */
  border: 0;
  border-radius: 7px;
  position: relative;
  transition: transform .45s;
  transform-style: preserve-3d;
}
.card--validPair {
  animation-name: disappear;
  -webkit-animation-name: disappear;
  animation-duration: .35s;
  -webkit-animation-duration: .35s;
  animation-fill-mode: forwards;
  -webkit-animation-fill-mode: forwards;
}
.card__face {
  width: 100%;
  height: 100%;
  position: absolute;
  backface-visibility: hidden;
}
.card__face--front {}
.card__face--back {
  transform: rotateY(180deg);
}
.card__face--back img {
  border-radius: 7px;
}
.card--selected {
  transform: rotateY(180deg);
}
</style>
