<template>
  <section class="container">
    <p class="title-text" :style="{ 
      transform: 'translate3d(' + skewX + 'px,' + skewY + 'px,' + skewZ + 'px) skew('+ skewX + 'deg,' + skewY + 'deg)', 
      transition: 8+'s' }">sarahachatz.com</p>
    <sound-control />
  </section>
</template>

<script>
import SoundControl from '~/components/SoundControl'

export default {
    data() {
    return {
      playMusic: false,
      music: null,
      skewX: 0,
      skewY: 0,
      skewZ: 0
    }
  },
  // mounted() {
  //     setInterval(() => {
  //       setTimeout(() => {
  //         this.skewX = Math.floor(Math.random() * 101) - 50;
  //       },3000)
  //       this.skewY = Math.floor(Math.random() * this.skewY) - 10;
  //       this.skewZ = Math.floor(Math.random() * 150) - 75;
  //       console.log(this.skewX)
  //     },8000)
  // },
  components: {
    SoundControl
  },
}
</script>

<style lang="scss">
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  animation: back-strobe 60*15s ease-in-out;
  animation-direction: normal;
  animation-iteration-count: infinite;
  animation-fill-mode: forwards;
  // background-image: linear-gradient(to bottom, transparent, #ffffff);
  background-image: radial-gradient(circle, #fff, transparent);
}

.title-text {
  font-size: 24px;
  font-weight: 200;
  // color: rgb(163,83,133);
  animation: text-strobe-style 100*20s ease-in-out, text-strobe-color 800s ease-in-out;
}

$p: 0%;
$color: 255;
$alpha: 1;
$letterSpacingMax: 50;
$shadowRandomHigh: 120;
$shadowRandomLow: 60;
$shadowBlurMax: 14;
$shadowAlphaMax: 1.0;
$shadowAlphaMin: (1.0)-0.4;

// @keyframes skew-change {
//   @for $x from 0 to 100 {
//     #{$p+$x} {transform: skewX((random($skewXMax))+deg)}
//   }
// }

@keyframes back-strobe {
  @for $x from 0 to 100 {
  #{$p+$x} {background-color: rgba(random($color), random($color), random($color), $alpha);}
  }
}

@keyframes text-strobe-style {
  @for $x from 0 to 100 {
  #{$p+$x} {
    text-shadow: (random($shadowRandomHigh)-$shadowRandomLow)+px (random($shadowRandomHigh)-$shadowRandomLow)+px random($shadowBlurMax)+px rgba(random($color), random($color), random($color), $shadowAlphaMin);
    letter-spacing: random($letterSpacingMax)+px;
    }
  }
}

@keyframes text-strobe-color {
  @for $x from 0 to 100 {
  #{$p+$x} {
    color: rgba(random($color), random($color), random($color), $alpha);
    }
  }
}
</style>
