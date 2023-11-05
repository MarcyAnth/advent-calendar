<template>
  <div class="container">
    <p class="counter" v-if="counting">{{ counter }}</p>
    <p class="counter-placeholder" v-if="!counting">0</p>
    <h1 style=" position: absolute; top: 25%;" v-if="isButtonDisabled">Come back tomorrow for more!</h1>
    <button class="wheel-button" :disabled="isButtonDisabled" @click="generateRandomNumber"><span>Click for today's gift!</span></button>
    <h1 class="opened-numbers">Opened Presents</h1>
    <div>
    <div style="display: flex; gap: 20px; flex-wrap: wrap; justify-content: center;">  
    <div v-for="prizes in removedItems" :key="prizes.id" :class="{ showNumber: showNumber }" class="present">
    <div class="lid">
      <span></span>
    </div>
    <div class="promo">
        <h1>{{ prizes.id }}</h1>
    </div>
    <div class="box">
      <span></span>
      <span></span>
    </div>
  </div>
    </div>
  </div>
  </div>
</template>

<script>
import wheelData from '../../wheel-data.json';

export default {
  name: 'WheelSpinner',
  data() {
    return {
      randomNumber: 23,
      wheelArray: [],
      buttonClicked: false,
      currentDate: new Date().toLocaleDateString(),
      removedItems: [],
      counter: 0,
      counting: false,
      showNumber: false
    };
  },
  props: {},
  methods: {
    generateRandomNumber() {
      if (this.isButtonDisabled) {
        return;
      }

      const chosenOne = Math.floor(Math.random() * this.randomNumber);


      this.startCountdown();
      this.isButtonDisabled = true;

      setTimeout(() => {
        if (chosenOne >= 0 && chosenOne < this.wheelArray.length) {
          const removedItem = this.wheelArray.splice(chosenOne, 1)[0];
          this.randomNumber -= 1;
          this.removedItems.push(removedItem);
          localStorage.setItem("removedItems", JSON.stringify(this.removedItems));
          localStorage.setItem("wheelArray", JSON.stringify(this.wheelArray));
          this.buttonClicked = true;
          this.showNumber = true;
        }
      }, 5000); 
    },

    startCountdown() {
      this.counting = true;
      this.counter = 5;

      const intervalId = setInterval(() => {
        this.counter--;

        if (this.counter === 0) {
          clearInterval(intervalId);
          this.counting = false;
        }
      }, 1000);
    },

    checkForNewDay() {
      const currentDate = new Date().toLocaleDateString();
      if (currentDate !== this.currentDate) {
        this.buttonClicked = false;
        this.isButtonDisabled = false;
        this.currentDate = currentDate;
      }
    },
  },
  computed: {
    isButtonDisabled: {
      get() {
        return localStorage.getItem('isButtonDisabled') === 'true';
      },
      set(value) {
        localStorage.setItem('isButtonDisabled', value);
      },
    },
  },
    mounted() {
    this.checkForNewDay();
    setInterval(this.checkForNewDay, 60000);
    const storedWheelArray = localStorage.getItem('wheelArray');
    if (storedWheelArray) {
      this.wheelArray = JSON.parse(storedWheelArray);
    } else {
      this.wheelArray = wheelData;
    }

    const storedRemovedItems = localStorage.getItem('removedItems');
    if (storedRemovedItems) {
      this.removedItems = JSON.parse(storedRemovedItems);
    }
}
};
</script>

<style lang="scss">

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.opened-numbers {

  color: white;
  margin: 100px 0;
}

.wheel-button {
  background-color: #6a7045;
  border: 1px solid white;
  border-radius: 5px;
  color: white;
  height: 100px;
  width: 200px;
  filter: drop-shadow(0 0 10px white);
  cursor: pointer;
  span {
    font-size: 20px;
    letter-spacing: 2px;
    
  }

} 
.showNumber {
  animation: fade-in 5s;
  color: white;
  flex-basis: 10%;
}

.counter {
  color: white;
  font-size: 5rem;
}

.counter-placeholder {
  visibility: hidden;
  font-size: 5rem;
}

@keyframes fade-in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.present {
  width: 205px;
  margin: 0 auto;
}

.box, .lid {
  background:
    -webkit-radial-gradient(white 7.5%, transparent 7.55%),
    -webkit-radial-gradient(white 7.5%, transparent 7.55%),
  rgb(240, 58, 58);
  background-position: 0 0, 12.5px 12.5px;
  background-size: 25px 25px;
  position: relative;
  margin: 0 auto;
}

.box {
  width: 200px;
  height: 125px;
}

.lid {
  width: 200px;
  height: 35px; 
  box-shadow: 0.5px 1px 1.5px rgba(0, 0, 0, 0.2); 
  z-index: 1;
  padding: 0 1px;
  background-color: rgb(216, 52, 52);
  top: 0;
  left: 0;
  transition: 
    top ease-out 0.5s,
    left ease-out 0.5s,
    transform ease-out 0.5s;
}

.box span, .lid span {
  position: absolute;
  display: block;
  background: rgba(235, 199, 0, 0.8);
  box-shadow: 0.5px 1px 1.5px rgba(0, 0, 0, 0.1);
}

.box span:first-child {
  width: 100%;
  height: 30px;
  top: 40px;
}

.box span:last-child {
  width: 30px;
  height: 100%; 
  left: 85px; 
}

.lid span {
  width: 30px;
  height: 100%; 
  left: 86px;
}

.promo {
  font-size: 15px;
  color: white;
  text-align: center;
  position: relative;
  height: 0;
  top: 5px;
  transition: all ease-out 0.7s;
}

.promo p {
  font-size: 12px;
}

.promo h2 {
  font-size: 20px;
}


.present:hover .lid {
  top: -100px;
  transform: rotateZ(10deg);
  left: 10px;
}
.present:hover .promo {
  top: -80px;
}

</style>
