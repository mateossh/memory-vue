<template>
  <div class="card" @click="$emit('click')">
    <img :src="imageBase64" />
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
.card {
  width: 100px;
  height: 100px;
  background-color: red;
  margin: 0;
}
.card--selected {
  filter: invert(100%)
}
</style>
