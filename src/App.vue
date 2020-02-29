<template>
  <div id="app">
    <Header />
    <GameBoard />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import GameBoard from './components/GameBoard.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    GameBoard,
    Footer,
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Raleway&display=swap');

body {
  background-color: #f4dada;
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Raleway', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #233240;
  width: 100%;
  height: 100%;
  margin-top: 60px;
  background-color: #f4dada;
  user-select: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}
</style>
