<template>
  <div class="soundContainer">
    <h1>sound test</h1>
    <button @click="playSound">Play Sound</button>
    <button @click="stopSound">Stop Sound</button>
    <!-- <script src="https://unpkg.com/tone"></script>
    <script src="https://unpkg.com/@tonejs/ui"></script>-->
  </div>
</template>

<script>
import Tone from "tone";
export default {
  data() {
    return {
      oscStart: 0,
      soundOn: false,
      scales: {
        bluesScale: [277, 329, 369, 392, 415, 493],
        abMinor: [207, 233, 246, 138, 155, 164, 185],
        jazzEm: [164, 185, 196, 207, 220, 246, 277, 293],
        gBmPent: ["F#3", "A3", "B3", "C3", "C#3", "E3"],
        bluesEb: ["D#4", "F#4", "G#4", "A4", "A#4", "C#4"]
      },
      timeOptions: ["20", "16", "18", "22", "30"],
      currentNote: 0,
      currentTime: "4n"
    };
  },
  mounted() {},

  methods: {
    playSound() {
      var synthA = new Tone.DuoSynth({
        oscillator: {
          type: "fmsquare",
          modulationType: "sine",
          modulationIndex: 3,
          harmonicity: 3.4
        },
        envelope: {
          attack: 0.0000000003,
          decay: 5,
          sustain: 0.01,
          release: 0.1
        }
      }).toMaster();

      var synthB = new Tone.Synth({
        oscillator: {
          type: "triangle8"
        },
        envelope: {
          attack: .00002,
          decay: 5,
          sustain: 0.4,
          release: .01
        }
      }).toMaster();


      var loop = new Tone.Loop(function(time) {
        
        let notes = [164, 185, 196, 207, 220, 246, 277, 293]
        let rand = Math.floor(Math.random() * notes.length)
        console.log(time);
        console.log(rand);
        console.log(notes[rand]);
        synthA.triggerAttackRelease(notes[rand], "1m");
        // synthB.triggerAttackRelease(notes[rand], "1m", "1m");
        // synthA.triggerAttackRelease(notes[rand], "1m");
      }, "1m");



      loop.start();
      Tone.Transport.bpm.value = 160
      Tone.Transport.start();
    },
    stopSound() {
      console.log("stop sound");
      Tone.Transport.cancel();
    }
  }
};
</script>

<style lang="scss">
html {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.nav {
  position: absolute;
  top: 0;
}
a {
  text-decoration: none;
  color: #24305e;
}
a:hover {
  color: #fc4445;
}
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
