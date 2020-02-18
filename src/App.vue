<template>
  <div id="app">
    <Header />
    <GameBoard />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import GameBoard from './components/GameBoard.vue'

export default {
  name: 'App',
  components: {
    Header,
    GameBoard,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: gray;
}
</style>
