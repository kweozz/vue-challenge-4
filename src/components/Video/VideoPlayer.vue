<script setup>
const props = defineProps({
  videosrc: String,
});
</script>

<template>
  <div class="player">
    <video autoplay loop muted :src="videosrc"></video>
    <div class="player__controls">
      <a href="#" @click.prevent="$emit('prevVideo')">↑</a>
      <a href="#" @click.prevent="$emit('nextVideo')">↓</a>
      <!-- $emit praat met uw parent. van uw child naar uw parent -->
    </div>
  </div>
</template>

<style scoped>
video {
  max-height: 100vh;
  object-fit: cover;
}
.player {
  background-image: url(./assets/background.png);
  background-repeat: no-repeat;
  background-size: cover;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.player__controls {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 20px;
}
.player__controls a {
  text-decoration: none;
  color: white;
  background-color: rgb(181, 180, 180);
  font-size: 20px;
  text-align: center;
  padding: 5px 10.5px;
  font-size: large;
  border-radius: 25px;
  margin-left: 20px;
}
</style>
