<template>
  <div id="app">

    <img src="./assets/Airwaves.svg" class="airwaves" alt="airwaves graphic">
    <!-- <div class="wave"></div> -->
    <img src="./assets/Wave.svg" class="wave w1" alt="wave graphic"> 
    <img src="./assets/Wave.svg" class="wave w2" alt="wave graphic">
    <img src="./assets/Wave.svg" class="wave w3" alt="wave graphic">
    <img src="./assets/Wave.svg" class="wave w4" alt="wave graphic">
    <img src="./assets/Wave.svg" class="wave w5" alt="wave graphic">
    <img src="./assets/Logo.svg" class="head-logo" alt="lockedin logo">

      <div class="phone-frame">
        <img src="./assets/blackNotch.svg" class="phone-notch" alt="phone notch">
        <BeyondPlayer />
      </div>
      <h1 class="player-info">Listen to bassdrive radio on your phone or in your browser</h1>
      <h5 class="player-info"><img src="./assets/Arrow.svg" alt="arrow pointing left"> Click Play and try it out!</h5>

      <h1 class="pwa-info">Tune in anywhere</h1>
      <p class="pwa-info">You can use this site as an app on your phone – no need to download anyhing –  just visit this page and hit “Add to home screen”.</p>
      <div class="ios-preview">
        <h5>iOS</h5>
      </div>
      <div class="android-preview">
        <h5>Android</h5>
      </div>

    <footer>
      <span>Find this useful? Care to make it better? <a href="https://github.com/panev/beyond-pwa.git" target="_blank">Contribute!</a> Licensed under <a href="https://choosealicense.com/licenses/gpl-3.0/" target="_blank">GNU GPL 3.0</a></span>
      <span></span>
      <span>Follow / DM me on <a href="https://twitter.com/todorpanev" target="_blank">Twitter</a></span>
    </footer>

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

$c-primary: #203555;
$c-secondary: #55D9CC;

body,
html {
  padding: 0;
  margin: 0;
  overflow-x: hidden;
  overflow-y: scroll;
  padding-bottom: 200px;
}

* {
  box-sizing: border-box;
}

#app {
  font-family: 'PT Sans', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(12, 60px);
  grid-column-gap: 20px; 
  grid-template-rows: 
    [logo] 100px 
    [player-info] 580px 
    [pwa-info] 580px 
    [footer] 300px;
  ;
  grid-row-gap: 90px;

}

.head-logo {
  grid-column: 1 / 13;
  grid-row: logo;
  justify-self: center;
  z-index: 1;
  position: relative;
}

.airwaves {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  top: -1260px;
  z-index: -1;
  animation: airani linear 15s infinite;
  transform-origin: 0%;
}

.wave {
  position: absolute;
  z-index: 0;
  left: 50%;
  top: -445px;
  width: 510px;
  height: 510px;
  border-radius: 50%;
  transform: translateX(-50%) scale(1);
  opacity: 0.6;
  animation: emitt 15s infinite linear;
}

.w1 {
  animation-delay: 0s;
}

.w2 {
  animation-delay: 3s;
}

.w3 {
  animation-delay: 6s;
}

.w4 {
  animation-delay: 9s;
}

.w5 {
  animation-delay: 12s;
}

@keyframes emitt {
  0% {
    transform: translateX(-52%) scale(1);
    opacity: 0.6;
  }


  100% {
    transform: translateX(-52%) scale(3);
    opacity: 0;
  }
}

.phone-frame {
  background-color: $c-primary;
  grid-row: player-info;
  grid-column: 2 / 6;
  height: 530px;
  grid-column: 2 / 6;
  border-radius: 24px;
  border: 10px solid $c-primary;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: relative;

  & img {
    margin-top: -0.6px;
    z-index: 1;
  }

  &:after {
    content: '';
    background: url('./assets/phoneShadow.svg');
    width: 327px;
    height: 129px;
    position: absolute;
    bottom: -50px;
    overflow: visible;
    z-index: -1;
  }

}

.player-info {
  grid-column: 7 / 12;
  grid-row: player-info;
}

h1.player-info {
  margin-top: 150px;
}

h5.player-info {
  margin-top: 290px;
  
  & img {
    position: relative;
    top: -5px;
    left: -10px;
  }
}

h1 {
  font-family: 'PT Sans Caption', sans-serif;
  font-weight: 700;
  font-size: 30px;
  color: $c-primary;
}

h5 {
  font-size: 20px;
  color: #203555;
  font-weight: 300;
  color: $c-secondary;
}

p {
  font-size: 21px;
  color: $c-secondary;
}

.pwa-info {
  grid-column: 2 / 12;
  grid-row: pwa-info;
  text-align: center;
}

p.pwa-info {
  margin-top: 70px;
}


.ios-preview,
.android-preview {
  height: 300px;
  border-radius: 50%;
  background: hotpink;
  margin-top: 200px;
  border: 10px solid #fff;
  grid-row: pwa-info;
  position: relative;

  &:after {
    content: ' ';
    display: block;
    width: 350px;
    height: 350px;
    background: url('./assets/previewShadow.svg');
    position: absolute;
    top: -15px;
    left: -30px;
    z-index: -1;
  }

  & h5 {
    text-align: center;
    position: absolute;
    bottom: -110px;
    left: 50%;
    transform: translateX(-50%);
  }
}

.ios-preview {
  grid-column: 2 / 6;
}

.android-preview {
  grid-column: 8 / 12;
}


footer {
  grid-row: footer;
  border-top: 1px dashed rgba($c-primary, .10);
  grid-column: 1 / 13;
  text-align: center;
  padding-top: 50px;
  margin-top: 50px;

  & span {
    display: block;
    font-size: 16px;
    color: #B4B4B4;
    margin: 5px auto;

    & a {
      color: #999;
      font-weight: bold;
      text-decoration: underline;
    
      &:hover {
        color: #333;
      }
    }
  }
}


@media (max-width: 1024px) {

  #app {
    justify-content: center;
    grid-template-columns: 1fr;
    grid-column-gap: 0px; 
    grid-template-rows: calc(100% + 20px);
    grid-row-gap: 0px;
    height: calc(100% + 20px);
    overflow-y: hidden;
    overflow-x: hidden;
  }

  body, html {
    height: calc(100% + 20px);
    padding: 0;
    overflow-y: hidden;
    overflow-x: hidden;
  }

  .head-logo,
  .player-info,
  .pwa-info,
  .ios-preview,
  .android-preview,
  .phone-notch,
  .airwaves,
    footer {
      display: none;
  }

  .phone-frame {
    grid-column: 1;
    grid-row: 1;
    border: none;
    border-radius: 0;
    height: calc(100% + 20px);
    overflow-y: hidden;
    overflow-x: hidden;
    
    &:after {
      display: none;
    }
  }

  .player-container,
  .player-gradient,
  .player-gradient-playing {
    border-radius: 0;
    overflow-y: hidden;
    overflow-x: hidden;
  }
}

@media (max-height: 800px) {
  #app {
    grid-row-gap: 10px;
  }
}

</style>
