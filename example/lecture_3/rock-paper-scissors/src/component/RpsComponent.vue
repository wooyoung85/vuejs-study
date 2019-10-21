<template>
  <div>
    <div class="wrapper">
      <!-- <div id="rps" :style="{background: `url(https://data.ac-illust.com/data/thumbnails/02/026c1244c72a188dea98394af582ce24_t.jpeg) 340px 0`}"></div> -->
      <!-- <div id="rps" :style="{'background-image': 'url(' + require('./assets/img/rockpaperscissors.jpg') + ')', 'background-position':'-697px 0'}"></div> -->
      <div>
        <h1 style="text-align:center">컴퓨터</h1>
        <div class="rps" :style="computedRpsStyle" @click="toggleRps"></div>
      </div>
      <div class="versus">
        <p class="jumbo-text">VS</p>
      </div>
      <div>
        <h1 style="text-align:center">나</h1>
        <div class="mychoice" style="text-align:center">
          <button class="jumbo-text button red" @click="onClickButton('가위')">가위</button>
          <button class="jumbo-text button blue" @click="onClickButton('바위')">바위</button>
          <button class="jumbo-text button yellow" @click="onClickButton('보')">보</button>
        </div>
      </div>
      <div class="result" v-for="(result, index) in results" :key="index">
        <p v-if="result.round > 0" style="margin: 1px">
          {{result.round}}라운드 결과
          <span style="font-weight:bold">{{result.winorloss}}</span>
        </p>
      </div>
    </div>

    <div></div>
  </div>
</template>

<script>
const rspCoords = {
  바위: "0",
  가위: "-349px",
  보: "-697px"
};
let interval = null;

const computerChoice = imgCoord => {
  return Object.entries(rspCoords).find(function(v) {
    return v[1] === imgCoord;
  })[0];
};

export default {
  name: "IconButtons",
  data() {
    return {
      imgCoord: rspCoords.가위,
      results: [
        {
          round: 0,
          comchoice: "",
          mychoice: "",
          winorloss: ""
        }
      ],
      count: 0,
      runrps: true
    };
  },
  methods: {
    toggleRps() {
      if (this.runrps) {
        clearInterval(interval);
        this.runrps = false;
      } else {
        this.changeHand();
        this.runrps = true;
      }
    },
    changeHand() {
      interval = setInterval(() => {
        if (this.imgCoord === rspCoords.바위) {
          this.imgCoord = rspCoords.보;
        } else if (this.imgCoord === rspCoords.보) {
          this.imgCoord = rspCoords.가위;
        } else if (this.imgCoord === rspCoords.가위) {
          this.imgCoord = rspCoords.바위;
        }
      }, 100);
    },
    onClickButton(choice) {
      clearInterval(interval);
      var comChoice = computerChoice(this.imgCoord);
      var result = "";

      this.count += 1;

      if (choice === "바위") {
        if (comChoice === "가위") {
          result = "승";
        } else if (comChoice === "보") {
          result = "패";
        } else {
          result = "무";
        }
      }

      if (choice === "보") {
        if (comChoice === "바위") {
          result = "승";
        } else if (comChoice === "가위") {
          result = "패";
        } else {
          result = "무";
        }
      }

      if (choice === "가위") {
        if (comChoice === "보") {
          result = "승";
        } else if (comChoice === "바위") {
          result = "패";
        } else {
          result = "무";
        }
      }
      var rpsResult = {
        round: this.count,
        comchoice: comChoice,
        mychoice: choice,
        winorloss: result
      };
      this.results.push(rpsResult);

      setTimeout(() => {
        this.changeHand();
      }, 1000);
    }
  },
  computed: {
    computedRpsStyle() {
      return {
        backgroundImage:
          "url(" + require("../assets/img/rockpaperscissors.jpg") + ")",
        backgroundPosition: `${this.imgCoord}, 0`
      };
    }
  },
  created() {
    console.log("created!!");
    this.changeHand();
  },
  mounted() {
    console.log("mounted!!");
  },
  updated() {
    console.log("updated!!");
  },
  destroyed() {
    console.log("destroyed!!");
    clearInterval(interval);
  }
};
</script>

<style scoped>
.wrapper {
  display: grid;
  grid-template-columns: 33% 33% 33%;
  margin: 10px 30px 10px 30px;
}

.rps {
  margin-left: auto;
  margin-right: auto;
  width: 340px;
  height: 340px;
  background-position: 0 0;
}
.versus {
  margin-top: 100px;
  text-align: center;
}

.mychoice {
  height: 340px;
  margin-top: 120px;
}
</style>