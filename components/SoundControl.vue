<template>
  <div class="sound-container" @click="musicControl">
    <span v-if="musicOn">
      <svg
        class="music-on"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:serif="http://www.serif.com/"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="100%"
        height="100%"
        style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:1.41421"
        version="1.1"
        viewBox="0 0 600 600"
        xml:space="preserve"
      >
        <path
          d="M125.058,190.896l-125.058,0l0,218.669l125.44,0l209.553,143.04l0,-505.21l-209.935,143.13l0,0.371Z"
          style="fill:#424344;fill-rule:nonzero"
        ></path>
        <path
          d="M485.687,312.335c0,-49.879 -26.906,-96.454 -70.222,-121.562c-11.284,-6.542 -25.749,-2.698 -32.301,8.609c-6.541,11.295 -2.698,25.749 8.598,32.301c28.783,16.667 46.653,47.575 46.653,80.652c0,33.088 -17.87,63.995 -46.642,80.663c-11.295,6.552 -15.15,21.006 -8.609,32.301c4.383,7.564 12.318,11.79 20.466,11.79c4.024,0 8.104,-1.023 11.824,-3.181c43.327,-25.085 70.233,-71.671 70.233,-121.573Z"
          style="fill:#424344;fill-rule:nonzero"
        ></path>
        <path
          d="M468.042,83.933c-13.397,-7.743 -30.537,-3.18 -38.292,10.206c-7.755,13.385 -3.181,30.525 10.205,38.28c64.153,37.157 104.018,106.097 104.018,179.916c0,73.818 -39.865,142.77 -104.018,179.927c-13.386,7.755 -17.96,24.895 -10.205,38.28c5.204,8.98 14.6,13.982 24.265,13.982c4.766,0 9.587,-1.214 14.027,-3.777c81.393,-47.148 131.958,-134.667 131.958,-228.412c0,-93.746 -50.565,-181.265 -131.958,-228.402Z"
          style="fill:#424344;fill-rule:nonzero"
        ></path>
      </svg>
    </span>
    
    <span v-else>
      <svg
        class="music-off"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:serif="http://www.serif.com/"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        width="100%"
        height="100%"
        style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:1.41421"
        version="1.1"
        viewBox="0 0 600 600"
        xml:space="preserve"
      >
        <path
          d="M9.48,174.721l0,257.099l147.485,0l246.383,168.18l0,-100.007l-325.259,-325.272l-68.609,0Z"
          style="fill:#424344;fill-rule:nonzero"
        ></path>
        <path
          d="M579.034,499.253l-175.686,-175.685l0,-317.569l-188.834,128.748l-123.237,-123.251c-15.329,-15.328 -40.185,-15.328 -55.514,0c-15.316,15.316 -15.316,40.172 0,55.501l487.77,487.757c7.651,7.664 17.708,11.497 27.75,11.497c10.043,0 20.087,-3.833 27.751,-11.497c15.315,-15.329 15.315,-40.185 0,-55.501Z"
          style="fill:#424344;fill-rule:nonzero"
        ></path>
      </svg>
    </span>
  </div>
</template>

<script>
import { Howl, Howler } from "howler";
export default {
  data() {
    return {
      musicOn: false,
      backgroundMusic: null
    };
  },
  mounted: function() {
    console.log("zomg ♥")
    this.backgroundMusic = new Howl({
      src: "background-music.mp3",
      loop: true,
      volume: 0.5
    });
  },
  methods: {
    musicControl() {
      this.musicOn = !this.musicOn;
      if (this.musicOn === true) {
        this.backgroundMusic.play();
      } else {
        this.backgroundMusic.pause();
      }
    }
  }
};
</script>

<style lang="scss">
.sound-container {
  width: 18px;
  position: absolute;
  top: 20px;
  right: 20px;
  cursor: pointer;
  svg * {
    fill: rgba(255, 255, 255, 0.2) !important;
    stroke: rgba(255, 255, 255, 0.2) !important;
    transition: 0.25s;
  }
  &:hover {
    svg * {
      fill: rgba(255, 255, 255, 0.6) !important;
      stroke: rgba(255, 255, 255, 0.6) !important;
      transition: 0.25s;
    }
  }
}
</style>
