<template>
  <div @keydown.space="spaceToggle" class="player-container" ref="playerContainer" tabindex="0">

    <audio ref="bdPlayer" id="bdplayer" src="https://bassdrive.radioca.st/;stream/1">
    </audio>

    <!-- Title -->
    <h2>{{ nowPlaying }}</h2>
    
    <input @input="handleVolume" v-model="bdPlayerVolume" type="range" min="0.1" max="1.0" step="0.01">
    
    <!-- Play button -->
    <transition name="transform">
      <button class="playButton" @click="bdPlay" v-show="!isPlaying">
        <img src="../assets/playerPlay.svg" alt="">
      </button>
    </transition>

    <!-- Pause button -->
    <transition name="transform">
      <button class="pauseButton" @click="bdPause" v-show="isPlaying">
        <img src="../assets/playerPause.svg" alt="">
      </button>
    </transition>

    <!-- Gradients -->
    <transition name="fade">
      <div class="player-gradient" v-show="!isPlaying"></div>
    </transition>

    <transition name="fade">
      <div class="player-gradient-playing" v-show="isPlaying"></div>
    </transition>


  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'BeyondPlayer',
  data: function() {
    return {
      isPlaying: false,
      nowPlaying: '',
      bdPlayerVolume: 0.5
    }
  },
  methods: {
    setStreamTitle() {
      axios
        .get('https://bassdrive.radioca.st/currentsong?sid=1')
        .then(response => this.nowPlaying = response.data) 
    },

    spaceToggle() {
      console.log(this.bdPlayerVolume)
      // This is a manual toggle-like implementation for the Space keypress event
      if (this.isPlaying == true) {
        this.bdPause();
      }

      else {
        this.bdPlay();
      }

    },

    handleVolume() {
      this.$refs.bdPlayer.volume=this.bdPlayerVolume;
    },

    bdPlay() {
      // Set volume & play
      this.handleVolume();
      this.$refs.bdPlayer.play();
      this.isPlaying = true;
      // Get & set stream title
      this.setStreamTitle();
      // Focus on the container, needed for the space key listner 
      this.$refs.playerContainer.focus();

    },

    bdPause() {
      // Pause playing
      this.$refs.bdPlayer.pause();
      this.isPlaying = false;
      // Focus on the container, needed for the space key listner
      this.$refs.playerContainer.focus();
    }
  },

  created() {
    this.setStreamTitle();
  },

  mounted() {
    this.$refs.playerContainer.focus();
  }
}
</script>

<style lang="scss">

input[type="range"] {
  position: absolute;
  top: 200px;
  z-index: 2000;
  -webkit-appearance: none;
  width: 50%; /* Specific width is required for Firefox. */
  background: transparent; /* Otherwise white in Chrome */
}

input[type="range"] {
  color: hotpink;
  margin: 0 auto;
  display: block;
  top: 85%;
  left: 50%;
  transform: translate(-45%, -50%);
  text-align: center;
}

input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none;
}

input[type=range]:focus {
  outline: none; 
}

input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none;
  border: 1px solid rgba(0,0,0,0.1);
  height: 38px;
  width: 38px;
  border-radius: 50%;
  background: #ffffff;
  cursor: pointer;
  margin-top: -16px;
  box-shadow: 6px 6px 6px rgba(0,0,0,0.3);
  transform-origin: center center;
  transition: 0.3s;
}

input[type=range]:active::-webkit-slider-thumb {
  box-shadow: 6px 6px 6px rgba(0,0,0,0.3), 
              0px 0px 20px rgba(255,255,255,0.5);
  transform: scale(1.5);
}

input[type=range]::-webkit-slider-runnable-track {
  width: 100%;
  height: 10px;
  cursor: pointer;
  box-shadow: 2px 2px 3px rgba(0,0,0,0.1);
  background: rgba(255,255,255,0.6);
  border-radius: 5px;
}

.player-container {
  width: 100%;
  height: 100%;
  background: url('../assets/playerBackground.jpg');
  background-size: cover; 
  position: absolute;
  z-index: 0;
  border-radius: 24px;
  box-shadow: inset 0px 0px 0px 6px rgba(32,53,85,0.2);


  &:focus {
    outline: none;
  }

  & h2 {
    position: absolute;
    z-index: 1;
    color: #fff;
    font-weight: 300;
    font-size: 18px;
    font-family: 'PT Sans Caption', sans-serif;
    top: 65px;
    left: 50%;
    transform: translateX(-50%);
    text-align: center;
    max-width: 90%;
    width: 90%;
    text-shadow: 2px 2px 2px rgba(0,0,0,0.2);
  }
}

.player-gradient {
  border-radius: 24px;
  width: 100%;
  height: 100%;
  opacity: 0.8;
  position: absolute;
  background-image: linear-gradient(-155deg, rgba(40,184,235,0.75) 0%, rgba(59,32,111,0.90) 100%);
}

.player-gradient-playing {
  border-radius: 24px;
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0.8;
  background-image: linear-gradient(-135deg, rgba(46,219,141,0.83) 0%, rgba(0,75,145,0.78) 100%);
}

button {
  position: absolute;
  z-index: 1;
  background: none;
  border: none;
  top: 50%;
  left: 50%;
  transform: translate(-45%, -50%);
  text-align: center;
  
  &:focus {
    outline: none;
  }

  &:hover {
    cursor: pointer;
  }

  & img {
    display: block;
  }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .35s;
}
.fade-enter, .fade-leave-to  {
  opacity: 0;
}

.transform-enter-active, .transform-leave-active {
  transition: transform .35s;
}
.transform-enter, .transform-leave-to {
  transform: translate(-45%, -50%) scale(0.1);
  opacity: 0;
}



</style>
