<template>
  <div class="container">
    <div class="wrapper">
      <div class="ctrlButtons">
        <div class="counter">{{this.shapes.length}}</div>
        <div class="plus" @click="newShape()">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            xmlns:serif="http://www.serif.com/"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            width="100%"
            height="100%"
            style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:1.41421"
            version="1.1"
            viewBox="0 0 1000 1000"
            xml:space="preserve"
          >
            <path
              class="back"
              d="M1000,500.005c0,276.141 -223.854,499.995 -500.005,499.995c-276.141,0 -499.995,-223.854 -499.995,-499.995c0,-276.141 223.854,-500.005 499.995,-500.005c276.151,0 500.005,223.864 500.005,500.005Z"
              style="fill:#757575;fill-rule:nonzero"
            ></path>
            <path
              class="front"
              d="M844.599,563.829l-280.77,0l0,280.78l-127.658,0l0,-280.78l-280.77,0l0,-127.658l280.77,0l0,-280.77l127.658,0l0,280.77l280.77,0l0,127.658Z"
              style="fill:#fff;fill-rule:nonzero"
            ></path>
          </svg>
        </div>
        <div class="minus" @click="arrPop()">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            xmlns:serif="http://www.serif.com/"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            width="100%"
            height="100%"
            style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:1.41421"
            version="1.1"
            viewBox="0 0 1000 1000"
            xml:space="preserve"
          >
            <path
              class="back"
              d="M1000,500.005c0,276.141 -223.854,499.995 -499.995,499.995c-276.141,0 -500.005,-223.854 -500.005,-499.995c0,-276.141 223.864,-500.005 500.005,-500.005c276.141,0 499.995,223.864 499.995,500.005Z"
              style="fill:#757575;fill-rule:nonzero"
            ></path>
            <rect
              class="front"
              width="689.198"
              height="127.658"
              x="155.38"
              y="436.171"
              style="fill:#fff;fill-rule:nonzero"
            ></rect>
          </svg>
        </div>
      </div>

      <div
        v-for="(tri, index) in shapes"
        :key="tri.index"
        class="clip"
        :style="{
        clipPath: 'polygon(' + tri.tr.r1 + '%' + tri.tr.r2 + '%,' + tri.tr.r3 + '%' + tri.tr.r4 + '%,' + tri.tr.r5 + '%' + tri.tr.r6 + '%)',
        backgroundColor: 'rgba(' + colors[index].r + ', ' + colors[index].g + ', ' + colors[index].b + ', ' + 0 + '.' + colors[index].a + ')',
        transition: 10 + 's linear'
      }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      shapes: [],
      colors: [],
      shapeCount: 0,
      startNum: 0
    };
  },
  mounted() {
    for (var q = 0; q < this.startNum; q++) {
      this.newShape();
    }

    setTimeout(() => {
      this.testRand(0, 100);
    }, 100);

    setInterval(() => {
      this.testRand();
    }, 10000);

    setInterval(() => {
      this.newColors2();
    }, 8000);
  },
  methods: {
    arrPop() {
      this.shapes.pop();
      this.colors.pop();
    },
    updateNewShape() {
      setTimeout(() => {
        this.randObjValues(0, 100, this.shapes.slice(-1)[0].tr);
      }, 10);
    },
    testRand() {
      for (var i = 0; i < this.shapes.length; i++) {
        this.randObjValues(0, 100, this.shapes[i].tr);
      }
    },
    newColors2() {
      for (var i = 0; i < this.colors.length; i++) {
        this.randObjValues(0, 255, this.colors[i]);
      }
    },
    newShape() {
      let shapeNum = this.shapeCount;
      shapeNum++;
      let newObj = {};
      newObj["tr"] = {
        r1: this.randNum(0, 100),
        r2: this.randNum(0, 100),
        r3: this.randNum(0, 100),
        r4: this.randNum(0, 100),
        r5: this.randNum(0, 100),
        r6: this.randNum(0, 100),
        update: this.randNum(5000, 10000)
      };
      let cObj = {};
      cObj = {
        r: this.randNum(0, 255),
        g: this.randNum(0, 255),
        b: this.randNum(0, 255),
        a: this.randNum(0, 100)
      };
      this.shapes.push(newObj);
      this.colors.push(cObj);
      this.updateNewShape();
      this.shapeCount = shapeNum;
    },
    randNum(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
    randObjValues(min, max, obj) {
      for (var rand in obj) {
        min = Math.ceil(min);
        max = Math.floor(max);
        obj[rand] = Math.floor(Math.random() * (max - min + 1)) + min;
      }
    },
    randTrans(min, max) {
      for (var rand in this.trans3d) {
        min = Math.ceil(min);
        max = Math.floor(max);
        this.trans3d[rand] = Math.floor(Math.random() * (max - min + 1)) + min;
      }
    }
  }
};
</script>

<style lang="scss">
.clip {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
}

.ctrlButtons {
  display: flex;
  position: absolute;
  top: 0.5rem;
  left: 0.8rem;
}

.ctrlButtons svg {
  width: 20px;
  margin: 0 5px;
  cursor: pointer;
  transition: 0.3s;
  & .front {
    fill: rgba(255, 255, 255, 0.3) !important;
    transition: all 0.3s ease;
  }
  & .back {
    fill: rgba(255, 255, 255, 0) !important;
    transition: all 0.3s ease;
  }
  &:hover {
    .front {
      fill: rgba(255, 255, 255, 0.6) !important;
      transition: all 0.3s ease;
    }
    .back {
      fill: rgba(255, 255, 255, 0) !important;
      transition: all 0.3s ease;
    }
    filter: drop-shadow(3px 3px 3px rgba(0, 0, 0, 0.15));
    transition: 0.3s;
  }
  &:active {
    transform: scale(0.8);
    transform: 0.15s;
  }
}
.counter {
  margin-right: 0.5rem;
  color: rgba(255, 255, 255, 0.3);
  font-weight: 900;
  font-size: 1.2em;
}
</style>
