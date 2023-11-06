<template>
    <div>
    <div class="audio-buttons">
    <audio id="player" v-bind:src="currentAudioUrl"></audio>
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
      currentAudioIndex: 0,
      audioData: require('../../audio-data.json'),
    };
  },

  computed: {
    currentAudioUrl() {
      if (this.currentAudioIndex >= 0 && this.currentAudioIndex < this.audioData.length) {
        return this.audioData[this.currentAudioIndex].src;
      } else {
        return ''; 
      }
    },
  },

  methods: {
    changeAudioUrl() {
    const currentDate = new Date().toLocaleDateString();
    if (currentDate !== this.currentDate) {
      this.currentAudioIndex = (this.currentAudioIndex + 1) % this.audioData.length;
      this.currentDate = currentDate;
    }
  },
  },

  mounted() {
    this.currentAudioIndex = 0;
    this.changeAudioUrl();
    setInterval(this.changeAudioUrl, 86400000);
  },
};
</script>