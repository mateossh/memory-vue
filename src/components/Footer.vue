<template functional>
  <footer class="footer">
    Made by <a class="footer__link" href="#">Mateusz Ż</a>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.footer {
  margin: 32px 0;
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
  height: 1px;
  background-color: #233240;
}
</style>
