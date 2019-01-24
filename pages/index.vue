<template>
  <section class="container">
    <!-- <audio autoplay loop>
     <source src="https://soundimage.org/wp-content/uploads/2018/10/Time-Running-Out_Looping.mp3" type="audio/mpeg">
        <p>If you're reading this, audio isn't supported.</p>
    </audio> -->
    <p class="title-text">sarahachatz.com</p>
  </section>
</template>

<script>
import {Howl, Howler} from 'howler'

export default {
  mounted: function playSound() {
            var sound = new Howl({
                src: 'background-music.mp3',
                autoplay: true,
                loop: true,
                volume: 0.5,
                onend: function() {
                    console.log('Finished!');
                }
            });            
        },
  components: {
  }
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
  color: rgb(163,83,133);
  animation: text-strobe-style 100*20s ease-in-out, text-strobe-color 800s ease-in-out;
}

$alpha: 1;
$alpha2: 3;
$delay: 1;
$test: 0%;
$test2: 100%;
$shadow: 15px;

$color: 255;
$fontSizeMax: 80;
$letterSpacingMax: 70;
$shadowRandomHigh: 120;
$shadowRandomLow: 60;
$shadowBlurMax: 14;
$shadowAlphaMax: 1.0;
$shadowAlphaMin: (1.0)-0.4;

@keyframes back-strobe {
  @for $x from 0 to 100 {
  #{$test+$x} {background-color: rgba(random($color), random($color), random($color), $alpha)}
  }
}

@keyframes text-strobe-style {
  @for $x from 0 to 100 {
  #{$test+$x} {
    text-shadow: (random($shadowRandomHigh)-$shadowRandomLow)+px (random($shadowRandomHigh)-$shadowRandomLow)+px random($shadowBlurMax)+px rgba(random($color), random($color), random($color), $shadowAlphaMin);
    // font-size: random($fontSizeMax)+px;
    letter-spacing: random($letterSpacingMax)+px;
    }
  }
}

@keyframes text-strobe-color {
  @for $x from 0 to 100 {
  #{$test+$x} {
    color: rgba(random($color), random($color), random($color), $alpha);
    }
  }
}
</style>
