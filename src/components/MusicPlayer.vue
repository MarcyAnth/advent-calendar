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
  props: {
    newDay: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      audio: [require("../assets/Mariah-Carey.mp3"),
      require("../assets/wham.mp3"),
      require("../assets/whitechristmas.mp3"),
      require("../assets/darlene.mp3"),
      require("../assets/stay.mp3"),
      require("../assets/p.mp3"),
      require("../assets/rocking.mp3"),
      require("../assets/lenon.mp3"),
      require("../assets/elton.mp3"),
      require("../assets/driving.mp3"),
      require("../assets/ariana.mp3"),
      require("../assets/swifite.mp3"),
      require("../assets/waitresses.mp3"),
      require("../assets/ronnettes.mp3"),
      require("../assets/rundmc.mp3"),
      require("../assets/runrudoplh.mp3"),
      require("../assets/kelly.mp3"),
      require("../assets/weather.mp3"),
      require("../assets/louis.mp3"),
      require("../assets/stevie.mp3"),
      require("../assets/paul.mp3"),
      require("../assets/destiny.mp3"),
      require("../assets/invisible.mp3"),
      require("../assets/love.mp3"),
      require("../assets/rule.mp3")
     ],
      index: localStorage.getItem('musicIndex') || 0
    };
  },
  mounted() {
    if(this.newDay) {
      this.index = (this.index + 1) % this.audio.length;
      localStorage.setItem('musicIndex', this.index);
    }
  }
};
</script>