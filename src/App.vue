<template>
  <div v-bind:class="{ ios: platformiOS }" id="app"> 

    <img src="./assets/Airwaves.svg" class="airwaves" alt="airwaves graphic">
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
    <h1 class="player-info">Listen to bassdrive radio on your phone, desktop or browser</h1>
    <h5 class="player-info"><img src="./assets/Arrow.svg" alt="arrow pointing left"> Click Play and try it out!</h5>

    <h1 class="pwa-info">Listen as an app on your desktop
</h1>
    <p class="pwa-info">You can use this site as an app on your phone &ndash; no need to download anyhing &ndash;  just visit this page and hit “Add to home” screen from your phone's share ot options menu.</p>
    <div class="ios-preview">
      <img src="./assets/iOSexpl.png" alt="explanation how to add to home screen on ios">
      <h5 class="subtitle-h5">iOS</h5>
    </div>
    <div class="android-preview">
      <img src="./assets/androidexpl.png" alt="explanation how to add to home screen on ios">
      <h5 class="subtitle-h5">Android</h5>
    </div>
    <img class="pwa-info" src="./assets/pwaInfoBackground.svg" alt="pwa info graphic">

    <h1 class="desktop-info">Listen as an app on your desktop</h1>
    <p class="desktop-info">Similarly to the phone, you can use this site as an app in your computer. Just click the "Install" icon in Google Chrome's address bar.</p>
    <div class="desktop-preview">
      <img src="./assets/desktopexpl.png" alt="explanation how to add to home screen on ios">
      <h5 class="subtitle-h5">macOS & Windows</h5>
    </div>
    <img class="desktop-info" src="./assets/pwaInfoBackground.svg" alt="pwa info graphic">

    <footer>
      <span>Find this useful? Care to make it better? <a href="https://github.com/panev/beyond-pwa.git" target="_blank">Contribute!</a> Licensed under <a href="https://choosealicense.com/licenses/gpl-3.0/" target="_blank">GNU GPL 3.0</a></span>
      <span></span>
      <span>Follow / DM me on <a href="https://twitter.com/todorpanev" target="_blank">Twitter</a></span>
    </footer>

    <img class="easter-explainer-ios top" src="./assets/iOSexpl.png" alt="explanation how to add to home screen on ios">
    <img class="easter-explainer-ios bottom" src="./assets/iOSexpl.png" alt="explanation how to add to home screen on ios">

  </div>
</template>

<script>
import BeyondPlayer from './components/BeyondPlayer.vue'

export default {
  name: 'app',
  components: {
    BeyondPlayer
  },
  data: function() {
    return {
      platformiOS: false
    }
  },
  mounted: function() {
    this.getPlatform()
  }, 
  methods: {
    getPlatform() {
      if( /iPhone|iPod/i.test(navigator.userAgent) ) {
        this.platformiOS = true;
      }
    }
  }
}
</script>

<style lang="scss">

::selection {
  background: yellow;
}

$c-primary: #203555;
$c-secondary: #55D9CC;

.easter-explainer-ios {
  display: none;
}

body,
html {
  padding: 0;
  margin: 0;
  overflow-x: hidden;
}

html {
  overflow-y: scroll; 
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
    [desktop-info] 580px 
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
  grid-row: player-info;
  grid-column: 2 / 6;
  height: 530px;
  grid-column: 2 / 6;
  border-radius: 34px;
  border: 10px solid rgba(32,53,85,0.1);
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: relative;

  & img {
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

.desktop-info {
  grid-column: 2 / 12;
  grid-row: desktop-info;
  text-align: center;
  margin-top: 70px;
}

p.desktop-info {
  margin-top: 120px;
}

p.pwa-info {
  margin-top: 70px;
}

img.pwa-info,
img.desktop-info {
  grid-column: 1 / 13;
  z-index: -2;
  margin-top: 150px;
  position: relative;
}

img.desktop-info {
  transform: rotate(180deg);
}


.ios-preview,
.android-preview {
  height: 300px;
  border-radius: 50%;
  margin-top: 200px;
  grid-row: pwa-info;
  position: relative;
  border: 2px $c-secondary;
  background: #fff;
  transition: 0.3s;
  display: flex;
  justify-content: center;

  & img {
    align-self: center;
  }

  &:after {
    content: ' ';
    display: block;
    width: 350px;
    height: 350px;
    background: url('./assets/previewShadow.svg');
    opacity: 0.3;
    position: absolute;
    top: -5px;
    left: -30px;
    z-index: -1;
  }
}

.subtitle-h5 {
    text-align: center;
    position: absolute;
    bottom: -110px;
    left: 50%;
    font-weight: bold;
    transform: translateX(-50%);
}

.ios-preview {
  grid-column: 2 / 6;
  border-style: dashed solid;
}

.android-preview {
  grid-column: 8 / 12;
  border-style: solid dotted;
}

.desktop-preview {
  position: relative;
  grid-row: desktop-info;
  height: 300px;
  margin-top: 200px;
  background: #fff;
  border-radius: 64px;
  border: 2px $c-secondary;
  border-style: solid dashed;
  grid-column: 2 / 12;
  box-shadow: 0 25px 32px rgba(0,0,0,0.08);
  display: flex;
  justify-content: center;
  & img {
    align-self: center;

  }
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

  .easter-explainer-ios {
    position: fixed;
    z-index: -10;
    left: 50%;
    transform: translateX(-50%);
    display: none;
    &.bottom {
      bottom: 20px;
    }
    &.top {
      top: 20px;
    }
  }

  #app {
    justify-content: center;
    grid-template-columns: 1fr;
    grid-column-gap: 0px; 
    grid-template-rows: 100%;
    grid-row-gap: 0px;
    height: 100%;
    overflow-y: hidden;
    overflow-x: hidden;

    &.ios .easter-explainer-ios {
      display: block;
    }

  }

  body, html {
    height: 100%;
    height: calc(100% + env(safe-area-inset-top));
    padding: 0;
    overflow-y: hidden;
    overflow-x: hidden;
  }

  body {
    background: $c-primary;
  }

  .head-logo,
  .player-info,
  .pwa-info,
  .desktop-info,
  .ios-preview,
  .android-preview,
  .desktop-preview,
  .phone-notch,
  .airwaves,
  .wave,
  footer {
      display: none;
  }

  .phone-frame {
    grid-column: 1;
    grid-row: 1;
    border: none;
    border-radius: 0;
    height: 100%;
    overflow-y: hidden;
    overflow-x: hidden;
    background: none;
    
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
