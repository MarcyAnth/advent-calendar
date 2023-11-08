<template>
    <div>
    <DateChecker @new-day="handleNewDay" />
    <div class="audio-buttons">
    <audio id="player" v-bind:src="audio[index]"></audio>
    <button onclick="document.getElementById('player').play()"><span>Play</span></button>
    <button onclick="document.getElementById('player').pause()"><span>Pause</span></button>
    <button onclick="document.getElementById('player').muted=!document.getElementById('player').muted"><span>Mute/ Unmute</span></button>
</div>
    </div>
</template>

<script>

export default {
    name: 'MusicPlayer',
  data() {
    return {
      audio: [require("../assets/Mariah-Carey.mp3") ,require("../assets/wham.mp3"),require("../assets/whitechristmas.mp3") ],
      index: 0
    };
  },
    methods: {
      handleNewDay() {
        this.index = (this.index + 1) % this.audio.length;
      }
  },
};
</script>