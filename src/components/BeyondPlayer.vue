<template>
  <div class="player-container">
    <audio ref="bdPlayer" id="bdplayer" src="http://bassdrive.radioca.st:80/;stream/1" volume="0.1">
    </audio>
    <button class="playButton" @click="bdPlay" v-if="!isPlaying">
      <img src="../assets/playerPlay.svg" alt="">
    </button>
    <button class="pauseButton" @click="bdPause" v-if="isPlaying">
      <img src="../assets/playerPause.svg" alt="">
    </button>
    <transition name="fade">
      <div class="player-gradient" v-show="!isPlaying"></div>
    </transition>
    <transition name="fade">
      <div class="player-gradient-playing" v-show="isPlaying"></div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'BeyondPlayer',
  data: function() {
    return {
      isPlaying: false
    }
  },
  methods: {
    bdPlay() {
      this.$refs.bdPlayer.play();
      this.isPlaying = true;
    },
    bdPause() {
      this.$refs.bdPlayer.pause();
      this.isPlaying = false;
    }
  }
}
</script>

<style lang="scss">

.player-container {
  width: 100%;
  height: 100%;
  background: url('../assets/playerBackground.png');
  background-size: cover; 
  position: absolute;
  z-index: 0;
  border-radius: 12px;
}

.player-gradient {
  border-radius: 12px;
  width: 100%;
  height: 100%;
  opacity: 0.8;
  position: absolute;
  background-image: linear-gradient(-155deg, rgba(40,184,235,0.75) 0%, rgba(59,32,111,0.90) 100%);
}

.player-gradient-playing {
  border-radius: 12px;
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0.69;
  background-image: linear-gradient(-135deg, rgba(46,219,141,0.83) 0%, rgba(0,75,145,0.78) 100%);
}

button {
  position: absolute;
  z-index: 1;
  background: none;
  border: none;
  top: 50%;
  left: 50%;
  transform: translate(-46%, -50%);
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
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

</style>
