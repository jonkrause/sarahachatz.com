<template>
  <section
    class="container"
    :style="{ 
    backgroundColor: 'rgb(' + color.r + ',' + color.g + ',' + color.b + ')', 
    transition: 'background-color ' + 10+'s ease-in-out'
    }"
  >
    <input type="text" onClick="this.select()" v-model="mainTitle" class="input-box">
    <p
      class="title-text"
      :style="{
      letterSpacing: ls + 'px',
      color: 'rgb(' + textColor.r + ',' + textColor.g + ',' + textColor.b + ')',
      textShadow: textShadow.x + 'px ' + textShadow.y + 'px ' + textShadow.blur + 'px rgba(' + textShadow.rgbaR + ', ' + textShadow.rgbaG + ', ' + textShadow.rgbaB + ', ' + textShadow.rgbaAlpha + ')', 
      transform: 'translate3d(' + textTranslate.x + 'px,' + textTranslate.y + 'px,' + textTranslate.z + 'px) skew(' + textSkew.x + 'deg, ' + textSkew.y + 'deg)', 
      transition: 'letter-spacing ' + 20 + 's ease-in-out, color ' + 10+'s ease-in-out, text-shadow ' + 10+'s ease-in-out, transform ' + 15+'s ease-in-out'
    }"
    >{{mainTitle}}</p>
    <!-- <p class="title-text" :style="{ 
      transform: 'translate3d(' + skewX + 'px,' + skewY + 'px,' + skewZ + 'px) skew('+ skewX + 'deg,' + skewY + 'deg)', 
    transition: 8+'s' }">sarahachatz.com</p>-->
    <sound-control/>
  </section>
</template>

<script>
import SoundControl from "~/components/SoundControl";

export default {
  data() {
    return {
      mainTitle: "sarahachatz.com",
      newText: "",
      playMusic: false,
      music: null,
      color: { r: 200, g: 137, b: 177 },
      textColor: { r: 0, g: 0, b: 0 },
      maxColor: 255,
      ls: 10,
      maxLetterSpacing: 40,
      textShadow: {
        x: 0,
        y: 0,
        blur: 0,
        rgbaR: 0,
        rgbaG: 0,
        rgbaB: 0,
        rgbaAlpha: 0
      },
      maxTextShadow: 121,
      maxTextShadowHalf: 60,
      maxTextShadowBlur: 15,
      textShadowAlpha: 2,
      textTranslate: { x: 0, y: 0, z: 0 },
      textTranslateMax: 140,
      textSkew: { x: 0, y: 0 },
      maxSkewX: 40,
      maxSkewY: 40
    };
  },
  mounted() {
    this.randomColor(10 * 1000);
    this.randomSpacing(20 * 1000);
    this.randomTextColor(15 * 1000);
    this.randomTextShadow(10 * 1000);

    setTimeout(() => {
      this.randomTextTranslate(12 * 1000);
      this.randomSkew(14 * 1000);
    }, 60 * 1000);
  },
  computed: {
    editText: function() {
      return (this.mainTitle = this.newText);
    }
  },
  methods: {
    randomSkew(ms) {
      setInterval(() => {
        this.textSkew.x =
          Math.floor(Math.random() * this.maxSkewX) - this.maxSkewX / 2;
        this.textSkew.y =
          Math.floor(Math.random() * this.maxSkewY) - this.maxSkewY / 2;
        // Math.floor(Math.random() * this.maxTextShadow) - this.maxTextShadowHalf;
      }, ms);
    },
    randomTextTranslate(ms) {
      setInterval(() => {
        this.textTranslate.x =
          Math.floor(Math.random() * this.textTranslateMax) -
          this.textTranslateMax / 2;
        this.textTranslate.y =
          Math.floor(Math.random() * this.textTranslateMax) -
          this.textTranslateMax / 2;
        this.textTranslate.z =
          Math.floor(Math.random() * this.textTranslateMax) -
          this.textTranslateMax / 2;
      }, ms);
    },
    randomColor(ms) {
      setInterval(() => {
        this.color.r = Math.floor(Math.random() * this.maxColor);
        this.color.g = Math.floor(Math.random() * this.maxColor);
        this.color.b = Math.floor(Math.random() * this.maxColor);
      }, ms);
    },
    randomSpacing(ms) {
      this.ls = 30;
      setInterval(() => {
        this.ls = Math.floor(Math.random() * this.maxLetterSpacing);
      }, ms);
    },
    randomTextColor(ms) {
      setInterval(ms => {
        this.textColor.r = Math.floor(Math.random() * this.maxColor);
        this.textColor.g = Math.floor(Math.random() * this.maxColor);
        this.textColor.b = Math.floor(Math.random() * this.maxColor);
      }, ms);
    },
    randomTextShadow(ms) {
      setInterval(() => {
        this.textShadow.x =
          Math.floor(Math.random() * this.maxTextShadow) -
          this.maxTextShadowHalf;
        this.textShadow.y =
          Math.floor(Math.random() * this.maxTextShadow) -
          this.maxTextShadowHalf;
        this.textShadow.blur = Math.floor(
          Math.random() * this.maxTextShadowBlur
        );
        this.textShadow.rgbaR = Math.floor(Math.random() * this.maxColor);
        this.textShadow.rgbaG = Math.floor(Math.random() * this.maxColor);
        this.textShadow.rgbaB = Math.floor(Math.random() * this.maxColor);
        this.textShadow.rgbaAlpha = (Math.random() * (1.4 - 1.0) + 0.3).toFixed(
          2
        );
        // console.log(this.textShadow.rgbaR)
        // console.log(this.textShadow.rgbaG)
        // console.log(this.textShadow.rgbaB)
        // console.log(this.textShadow.x)
        // console.log(this.textShadow.y)
        // console.log(this.textShadow.blur)
        // console.log(this.textShadow.rgbaAlpha);
      }, ms);
    }
  },
  components: {
    SoundControl
  }
};
</script>

<style lang="scss">
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-image: radial-gradient(circle, #fff, transparent);
}

.title-text {
  font-size: 24px;
  font-weight: 200;
  color: rgb(163, 83, 133);
  // animation: text-strobe-style 100*20s ease-in-out, text-strobe-color 800s ease-in-out;
}
.input-box:focus {
  outline: 0;
  background-color: rgba(255, 255, 255, 0);
  color: rgba(255, 255, 255, 0.3);
  width: 150px;
  transition: 0.3s ease-in-out;
  overflow: visible;
  padding-bottom: 3px;
}
.input-box:hover {
  background-color: rgba(255, 255, 255, 0.3);
  transition: 0.3s;
}
.input-box::selection {
  color: pink;
}
.input-box {
  position: absolute;
  top: 18px;
  right: 50px;
  width: 20px;
  height: 20px !important;
  cursor: pointer;
  text-align: right;
  background-color: rgba(255, 255, 255, 0.05);
  height: 24px;
  border: inset 0;
  border: 0;
  // border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-size: 14px;
  color: transparent;
  padding: 0px 5px 0px 3px;
  transition: 0.3s;
}
</style>
