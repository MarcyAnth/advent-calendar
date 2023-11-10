<template>
  <div>
    <div 
      class="snow"
      v-for="i in SNOW_INTENSITY"
      :key="i"
    ></div>
  </div>
  <div class="heading-text">
    <img class="x-mas-tree" v-bind:src="christmasTree" />
    <h1>Merry Christmas Vicky... Ho, Ho,Ho.</h1>
    <img class="x-mas-tree" v-bind:src="christmasTree" />
  </div>
  <MusicPlayer v-if="newDay !== null" :newDay="newDay" />
  <WheelSpinner 
    :openedTodaysGift="openedTodaysGift" 
    @openGift="() => {this.openedTodaysGift = true}"
  />
</template>

<script>

import WheelSpinner from './components/WheelSpinner.vue'
import MusicPlayer from './components/MusicPlayer.vue'

const SNOW_INTENSITY = 200;

export default {
  name: 'App',
  components: {
    WheelSpinner, MusicPlayer  
  },
  data() {
    return {
      christmasTree: require("./assets/660-christmas-tree.svg"),
      SNOW_INTENSITY: SNOW_INTENSITY,
      openedTodaysGift: false,
      pageLoadedOn: localStorage.getItem('pageLoadedOn'),
      newDay: null
    }
  },
  mounted() {
    if (!this.pageLoadedOn) {
      this.pageLoadedOn = new Date().toLocaleDateString();
      localStorage.setItem('pageLoadedOn', this.pageLoadedOn);
    }
    
    if (this.pageLoadedOn !== new Date().toLocaleDateString()) {
      this.newDay = true;
      this.pageLoadedOn = new Date().toLocaleDateString();
      localStorage.setItem('pageLoadedOn', this.pageLoadedOn);
    } else {
      this.newDay = false;
    }

    this.openedTodaysGift = localStorage.getItem('lastGiftDate') === new Date().toLocaleDateString();
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Festive&family=Playpen+Sans&display=swap');
h1,h2,h3,h4,h5, button, p {
  margin: 0px;
  font-family: 'Festive', cursive;
  color: white;
}

body {
  background-color: #b71a3b;
}

@function random_range($min, $max) {
  $rand: random();
  $random_range: $min + floor($rand * (($max - $min) + 1));
  @return $random_range;
}

.audio-buttons {
  display: flex;
  gap: 10px;
  justify-content: center;
  button {
  background-color: #6a7045;
  border: 1px solid white;
  border-radius: 5px;
  color: white;
  cursor: pointer;
  span {
    font-size: 10px;
    letter-spacing: 1px;
  }
  }
}

.heading-text {
  margin-top: 50px;
  color: white;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;

  .x-mas-tree {
    width: 100px;
  }
}

.snow {
  filter: drop-shadow(0 0 10px white);
  $total: 200;
  position: absolute;
  width: 10px;
  height: 10px;
  background: white;
  border-radius: 50%;

  @for $i from 1 through $total {
    $random-x: random(1000000) * 0.0001vw;
    $random-offset: random_range(-100000, 100000) * 0.0001vw;
    $random-x-end: $random-x + $random-offset;
    $random-x-end-yoyo: $random-x + ($random-offset / 2);
    $random-yoyo-time: random_range(30000, 80000) / 100000;
    $random-yoyo-y: $random-yoyo-time * 100vh;
    $random-scale: random(10000) * 0.0001;
    $fall-duration: random_range(10, 30) * 1s;
    $fall-delay: random(30) * -1s;

    &:nth-child(#{$i}) {
      opacity: random(10000) * 0.0001;
      transform: translate($random-x, -10px) scale($random-scale);
      animation: fall-#{$i} $fall-duration $fall-delay linear infinite;
    }

    @keyframes fall-#{$i} {
      #{percentage($random-yoyo-time)} {
        transform: translate($random-x-end, $random-yoyo-y) scale($random-scale);
      }

      to {
        transform: translate($random-x-end-yoyo, 100vh) scale($random-scale);
      }
    }
  }
}


</style>
