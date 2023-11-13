<template>
<div class="reindeer">
  <div class="head">
    <div class="eyes-and-nose"></div>
    <div class="antlers">
      <div class="outside-antler-trunk right">
        <div class="antler-branches right"></div>
      </div>
      <div class="outside-antler-trunk left">
        <div class="antler-branches left"></div>
      </div>
      <div class="inside-antler right"></div>
      <div class="inside-antler left"></div>
    </div>
  </div>
  <div class="tail"></div>
  <div class="legs">
    <div class="leg-rear-right"></div>
    <div class="leg-rear-left"></div>
    <div class="leg-front-right"></div>
    <div class="leg-front-left"></div>
  </div>
  <div class="ground"></div>
</div>
</template>

<script>
export default {
  name: 'ReindeerBrown',
  components: {

  },
}
</script>


<style lang="scss">
// Transform
$scale: 1;
$rotate: -2deg;

// Colours
$body-colour: lighten(#CD9B65, 10%);
$head-colour: darken($body-colour, 0%);
$neck-colour: lighten($body-colour, 10%);
$tail-colour: darken($body-colour, 20%);
$eye-colour: #774916;
$antler-colour: #563107;
$nose-colour: #FF0000;

// Shadow
$shadow: 10%;

.reindeer {

  // Body
  transform: scale($scale) rotateZ($rotate);
  position: absolute;
  top: 60px;
  right: 0;
  bottom: 0;
  left: -71%;
  margin: auto;
  border-top: solid 25px transparent;
  border-right: solid 150px $body-colour;
  width: 0px;
  height: 60px;
  
  // Neck
  &:before {
    content: '';
    position: absolute;
    top: -25px;
    left: 150px;
    border-left: solid 50px $neck-colour;
    border-bottom: solid 40px transparent;
    width: 0px;
    height: 45px;
  }
  
  // Back of neck
  &:after {
    content: '';
    position: absolute;
    top: -50px;
    left: 150px;
    border-left: solid 20px transparent;
    border-bottom: solid 25px $neck-colour;
    width: 30px;
    height: 0px;    
    z-index: -1;
  }
}

.head {
  
  // Head
  content: '';
  position: absolute;
  top: -80px;
  left: 160px;
  background-color: $head-colour;
  border-radius: 0px 0px 15px 15px;
  width: 40px;
  height: 55px;
  animation: 10s tilt ease-in-out infinite;
  
  // Left ear
  &:before {
    content: '';
    position: absolute;
    top: -10px;
    left: -20px;
    border-left: solid 20px transparent;
    border-top: solid 20px $body-colour;
    width: 0px;
    height: 0px;
    z-index: 1;
  }
  
  // Right ear
  &:after {
    content: '';
    position: absolute;
    top: -10px;
    left: 40px;
    border-right: solid 20px transparent;
    border-top: solid 20px $body-colour;
    width: 0px;
    height: 0px;
    z-index: 1;
  }
}

.eyes-and-nose {
  
  // Nose
  width: 4px;
  height: 4px;
  border-radius: 50%;
  margin: 30px auto;
  background-color: $nose-colour;
  box-shadow: 0px 0px 4px 4px $nose-colour;
  animation: 5s glow infinite ease-in-out;
  
  // Right eye
  &:before {
    content: '';
    position: absolute;
    top: 18px;
    right: 4px;
    border-right: solid 6px transparent;
    border-top: solid 6px $eye-colour;
    width: 0px;
    height: 0px;
    animation: 5s blink infinite linear;
  }
  
  // Left eye
  &:after {
    content: '';
    position: absolute;
    top: 18px;
    left: 4px;
    border-left: solid 6px transparent;
    border-top: solid 6px $eye-colour;
    width: 0px;
    height: 0px;
    animation: 5s blink infinite linear;
  }
}

.antlers {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 65px;
  left: 0;
  margin: auto;
  
  &:before {
    content: '';
    top: 0px;
    position: absolute;
    width: 40px;
    height: 12px;
    background-color: $body-colour;
    z-index: 1;
  }
}

.outside-antler-trunk {
  
  // Root
  position: absolute;
  top: -50px;
  width: 8px;
  height: 60px;
  background-color: $antler-colour;
  transform-origin: 4px 52px;
  
  &.left {
    position: absolute;
    left: 0;
    transform: rotateZ(-45deg);
  }
  
  &.right {
    position: absolute;
    right: 0;
    transform: rotateZ(45deg) rotateY(180deg);
  }
  
  // Middle
  &:before {
    content: '';
    position: absolute;
    top: -45px;
    left: 10px;
    width: 8px;
    height: 50px;
    background-color: $antler-colour;
    transform: rotateZ(25deg);
  }
  
  // Top
  &:after {
    content: '';
    position: absolute;
    top: -63px;
    left: 32px;
    width: 8px;
    height: 30px;
    background-color: $antler-colour;
    border-radius: 4px 4px 0px 0px;
    transform: rotateZ(60deg);
  }
}

.antler-branches {
  position: absolute;
  top: -40px;
  width: 8px;
  height: 30px;
  background-color: $antler-colour;
  z-index: -1;
  border-radius: 4px 4px 0px 0px;
  transform-origin: 4px 35px;
  
  &.left {
    transform: rotateZ(55deg);
  }
  
  &.right {
    transform: rotateZ(55deg) rotateY(180deg);
  }
}
  
.inside-antler {
  position: absolute;
  top: -12px;
  width: 8px;
  height: 20px;
  background-color: $antler-colour;
  z-index: 1;
  transform-origin: 4px 0px;
  border-radius: 0px 0px 4px 4px;
  
  // Top
  &:before {
    content: '';
    position: absolute;
    top: -18px;
    left: 5px;
    width: 8px;
    height: 20px;
    background-color: $antler-colour;
    z-index: 1;
    transform-origin: 4px 0px;
    border-radius: 4px 4px 0px 0px;
    transform: rotateZ(15deg);
  }
  
  &.left {
    position: absolute;
    left: 3px;
    transform: rotateZ(-30deg);
  }
  
  &.right {
    position: absolute;
    right: 3px;
    transform: rotateZ(30deg) rotateY(180deg);
  }
}

.tail {
  content: '';
  position: absolute;
  top: -19px;
  left: -15px;
	border-top: 15px solid transparent;
	border-left: 20px solid $tail-colour;
  width: 0px;
  height: 0px;
  transform-origin: 20px 20px;
  transform: rotateZ(-75deg);
  animation: 15s flap ease-in-out infinite;
}

.legs {
  position: absolute;
  top: 59px;
  
  div {
    position: absolute;
  }
}

.leg-rear-right {
  
  // Hip
  width: 10px;
  border-top: 30px solid $body-colour;
	border-right: 45px solid transparent;
  z-index: 1;
  
  // Middle
  &:before {
    content: '';
    position: absolute;
    top: -40px;
    left: 5px;
    width: 10px;
    height: 70px;
    background-color: $body-colour;
    transform: rotateZ(55deg);
  }
  
  // Bottom
  &:after {
    content: '';
    position: absolute;
    top: 11px;
    left: -23px;
    width: 10px;
    height: 60px;
    background-color: $body-colour;
    transform: rotateZ(2deg);
    border-radius: 0px 0px 10px 10px;
  }
}

.leg-rear-left {
  
  // Hip
  width: 10px;
  left: 34px;
  border-top: 25px solid darken($body-colour, $shadow);
	border-right: 15px solid transparent;
  
  // Middle
  &:before {
    content: '';
    position: absolute;
    top: -5px;
    left: -6px;
    width: 10px;
    height: 30px;
    background-color: darken($body-colour, $shadow);
    transform: rotateZ(29deg);
  }
  
  // Bottom
  &:after {
    content: '';
    position: absolute;
    top: 16px;
    left: 0px;
    width: 10px;
    height: 60px;
    background-color: darken($body-colour, $shadow);
    transform: rotateZ(-25deg);
    border-radius: 0px 0px 10px 10px;
  }
}

.leg-front-right {
  
  // Shoulder
  width: 10px;
  left: 115px;
  border-top: 20px solid $body-colour;
	border-left: 25px solid transparent;
  z-index: 1;
  
  // Middle
  &:before {
    content: '';
    position: absolute;
    top: -3px;
    left: 2px;
    width: 10px;
    height: 30px;
    background-color: $body-colour;
    transform: rotateZ(-10deg);
  }
  
  // Bottom
  &:after {
    content: '';
    position: absolute;
    top: 24px;
    left: 11px;
    width: 10px;
    height: 60px;
    background-color: $body-colour;
    transform: rotateZ(-13deg);
    border-radius: 0px 0px 10px 10px;
  }
}

.leg-front-left {
  
  // Shoulder
  width: 10px;
  left: 110px;
  border-top: 20px solid darken($body-colour, $shadow);
	border-left: 15px solid transparent;
  
  // Middle
  &:before {
    content: '';
    position: absolute;
    width: 10px;
    height: 30px;
    left: 1px;
    top: -1px;
    background-color: darken($body-colour, $shadow);
    transform: rotateZ(-5deg);
  }
  
  // Bottom
  &:after {
    content: '';
    position: absolute;
    width: 10px;
    height: 55px;
    left: 6px;
    top: 27px;
    background-color: darken($body-colour, $shadow);
    transform: rotateZ(-8deg);
    border-radius: 0px 0px 10px 10px;
  }
}

.ground {
  background-color: #F5F5F5;
    width: 110vw;
    margin: auto;
    height: 100vh;
    position: absolute;
    top: 152px;
    right: -93vw;
    z-index: 0;
    transform: rotate(0deg);
}

body {
  margin: 0px;
  height: 100%;
  overflow: hidden;
}

@keyframes glow {
  0% {
    box-shadow: 0px 0px 4px 4px $nose-colour;
  }
  50% {
    box-shadow: 0px 0px 20px 10px $nose-colour;
  }
}

@keyframes blink {
  0% {
    top: 18px;
    border-top: solid 6px $eye-colour;
  }
  2% {
    top: 21px;
    border-top: solid 0px $eye-colour;
  }
  4% {
    top: 18px;
    border-top: solid 6px $eye-colour;
  }
  30% {
    top: 18px;
    border-top: solid 6px $eye-colour;
  }
  32% {
    top: 21px;
    border-top: solid 0px $eye-colour;
  }
  34% {
    top: 18px;
    border-top: solid 6px $eye-colour;
  }
}

@keyframes flap {
  0% {
    transform: rotateZ(-75deg);
  }
  1% {
    transform: rotateZ(-30deg);
  }
  2% {
    transform: rotateZ(-75deg);
  }
  3% {
    transform: rotateZ(-30deg);
  }
  4% {
    transform: rotateZ(-75deg);
  }
  68% {
    transform: rotateZ(-75deg);
  }
  69% {
    transform: rotateZ(-30deg);
  }
  70% {
    transform: rotateZ(-75deg);
  }
}

@keyframes tilt {
  0% {
    transform: rotateZ(0deg);
  }
  5% {
    transform: rotateZ(5deg);
  }
  15% {
    transform: rotateZ(5deg);
  }
  20% {
    transform: rotateZ(0deg);
  }
}
</style>