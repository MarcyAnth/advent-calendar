<template>
  <div :class="{modal: firstLoad}">
  </div>
  <div id="homepage" :class="{fadeIn: setAnimation}" v-if="firstLoad">
    <SantaPerson/>
    <div id="welcome-box">
      <h1>Welcome Vicky!</h1>
      <p>You are now going to start your 2023 Advent Calendar journey...</p>
      <p>Each day you can press the button to get a present. Each present will have a number assigned to it. That will be the one you can open :D (Exactly what you done for me last year lol)</p>
      <p>Please do not refresh your local storage, or clear cache. If you need to do for other reasons, please contact techincal support (Me.)</p>
      <p>Every day there is also a song of the day, the controls to play are under the title when you enter. It may be quite loud so turn the volume down before!</p>
      <button id="welcome-button" @click="closeWelcome"><span>Enter</span></button>
    </div>
  </div>
  </template>
  <script>
  
  import SantaPerson from './Santa.vue'

  export default {
  name: 'SantaModa',
  components: {
    SantaPerson
  },
  props: {
  },
  data() {
    return {
      firstLoad: true,
      setAnimation: false
    }
  },
  methods: {
    closeWelcome(){
      localStorage.setItem('welcomeMessage', 'false');
      this.setAnimation = true
      setTimeout(() => {
        this.firstLoad = false;
        location.reload()
      }, 1000);
    }
  },
  mounted() {
    if (localStorage.getItem('welcomeMessage') === null) {
      localStorage.setItem('welcomeMessage', 'true');
    }

    this.firstLoad = localStorage.getItem('welcomeMessage') === 'true';
    this.$emit('first-load', this.firstLoad);
  },
}
  </script>
  
<style lang="scss">

.fadeIn {
  animation: fade-out 1s;
}

button {
  background-color: #6a7045;
  border: 1px solid white;
  border-radius: 5px;
  color: white;
  cursor: pointer;
  span {
    font-size: 18px;
    letter-spacing: 1px;
  }
  }

  #welcome-box {
    position: absolute;
    top: 56%;
    left: 14%;
    background-color: white;
    width: 75%;
    border: 1px solid;
    border-radius: 5px;
    z-index: 999;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;

    #welcome-button {
      text-align: center;
      padding: 10px;
      margin: 10px;
      width: 200px;
      span {
        font-size: 18px;
      }
    }

    h1 {
      color: #b71a3b;
      text-align: center;
      font-family: 'Playpen Sans', cursive;
    }

    p {
      color: #6a7045;
      font-size: 1.5rem;
      letter-spacing: 1px;
      text-align: center;
      font-family: 'Playpen Sans', cursive;
    }
  }


.modal {
    height: 1200px;
    width: 110%;
    opacity: 0.5;
    background-color: white;
    position: absolute;
    top: 0%;
    z-index: 999;
    left: 0%;
}

  
  </style>