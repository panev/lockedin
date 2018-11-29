<template>
  <div class="player-container">

    <audio ref="bdPlayer" id="bdplayer" src="http://bassdrive.radioca.st:80/;stream/1" volume="0.1">
    </audio>
<!-- Future feature -->
<!-- <h2>{{ nowPlaying }}</h2> -->
    <transition name="transform">
      <button class="playButton" @click="bdPlay" v-show="!isPlaying">
        <img src="../assets/playerPlay.svg" alt="">
      </button>
    </transition>

    <transition name="transform">
      <button class="pauseButton" @click="bdPause" v-show="isPlaying">
        <img src="../assets/playerPause.svg" alt="">
      </button>
    </transition>

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
      isPlaying: false,
      nowPlaying: ''
    }
  },
  mounted: function() {
    this.scrollBy();
  },
  methods: {
    // Future feature (Showing the now-laying title, blocked by CORS issue)
    // setStreamTitle() {
    //   var req = new XMLHttpRequest();

    //   req.open('GET', 'http://shouthost.com.32-1.streams.bassdrive.com:8200/7.html', true);

    //   req.onreadystatechange = function () {
    //     if (this.readyState == 4 && this.status == 200) {
    //       var bdNowPlaying = this.responseText.match('<body>(.+)<\/body>')[1];
    //       var bdNowPlayingTitle = bdNowPlaying.split(',');
    //       this.nowPlaying = bdNowPlayingTitle[6];
    //       console.log(bdNowPlayingTitle[6]);
    //     }
    //   }
    //   req.send();
    // },
    scrollBy() {
      window.scrollBy(0, 40);
    },
    bdPlay() {
      this.$refs.bdPlayer.play();
      this.isPlaying = true;
      // Future feature
      // this.setStreamTitle();
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

  & h2 {
    position: absolute;
    z-index: 1;
    color: #fff;
    font-weight: 300;
    font-size: 14px;
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
