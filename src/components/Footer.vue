<template>
  <footer class="footer">
    <div class="footer__text--left">Moves: {{ movesCounter }}</div>
    <div class="footer__text--right">
      Made by <a class="footer__link" href="https://mateossh.me" target="_blank" rel="noopener noreferrer">Mateusz</a> | <a class="footer__link" href="https://github.com/mateossh/memory" target="_blank" rel="noopener noreferrer">Source code</a>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  props: {
    movesCounter: Number,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.footer {
  margin: 32px 12px;
  display: flex;
  justify-content: space-between;
}

.footer__link {
  color: inherit;
  text-decoration: none;
  position: relative;
}

.footer__link:after {
  content: '';
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  margin: auto;
  width: 86%;
  height: 2px;
  background-color: #233240;
}
</style>
