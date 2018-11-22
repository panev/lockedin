<template>
  <div id="app">
    <img src="./assets/Airwaves.svg" class="airwaves" alt="airwaves graphic">
    <img src="./assets/Logo.svg" class="head-logo" alt="lockedin logo">
    <BeyondPlayer />
  </div>
</template>

<script>
import BeyondPlayer from './components/BeyondPlayer.vue'

export default {
  name: 'app',
  components: {
    BeyondPlayer
  }
}
</script>

<style lang="scss">

body,
html {
  padding: 0;
  margin: 0;
  overflow-x: hidden;
  overflow-y: scroll;

}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(12, 60px);
  grid-column-gap: 20px; 
}

.head-logo {
  grid-column: 1 / 13;
  justify-self: center;
}

.airwaves {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: -1550px;
  z-index: -1;
  animation: airani linear 15s infinite;
  transform-origin: 0%;
}

/*@keyframes airani {
  0% {
    transform: scale(1) translateX(-50%);
  }

  100% {
    transform: scale(2) translateX(-50%);
  }
}
*/
</style>
