<template>
  <div>
    <audio ref="bdPlayer" id="bdplayer" src="http://bassdrive.radioca.st:80/;stream/1" volume="0.1">
    </audio>
    <button @click="bdPlay">play/pause</button>
  </div>
</template>

<script>
export default {
  name: 'BeyondPlayer',
  methods: {
    bdPlay() {
      this.$refs.bdPlayer.play();
    },
    bdPause() {
      this.$refs.bdPlayer.pause();
    }
  }
}
</script>

<style scoped lang="scss">

</style>
