<template>
  <div>
    <h1 class="center-text">
      가위바위보 게임
      <button
        class="button middle-text"
        :class="{gray:rungame, green:!rungame}"
        @click="toggleGame"
      >{{buttonMessage}}</button>
    </h1>

    <rps-component v-if="rungame"></rps-component>
  </div>
</template>

<script>
import rpsComponent from "@/components/RpsComponent.vue";
export default {
  components: { rpsComponent },
  data() {
    return {
      rungame: false
    };
  },
  methods: {
    toggleGame() {
      if (this.rungame) {
        this.rungame = false;
      } else {
        this.rungame = true;
      }
    }
  },
  computed: {
    buttonMessage() {
      if (this.rungame) {
        return "종료하기";
      } else {
        return "시작하기";
      }
    }
  }
};
</script>

<style scope>
.center-text {
  text-align: center;
}
.jumbo-text {
  font-size: 50px;
}
.middle-text {
  font-size: 25px;
}
.button {
  margin: 3px;
  position: relative;
  border: none;
  color: #ffffff;
  text-align: center;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;
  text-decoration: none;
  overflow: hidden;
  cursor: pointer;
}
.button:after {
  content: "";
  background: #f1f1f1;
  display: block;
  position: absolute;
  padding-top: 300%;
  padding-left: 350%;
  margin-left: -20px !important;
  margin-top: -120%;
  opacity: 0;
  transition: all 0.8s;
}
.button:active:after {
  padding: 0;
  margin: 0;
  opacity: 1;
  transition: 0s;
}
.result {
  grid-column-start: 1;
  grid-column-end: 4;
  margin-left: 100px;
}
.yellow {
  background-color: #ffe000;
}
.blue {
  background-color: #008cba;
}
.red {
  background-color: #f44336;
}
.green {
  background-color: #4caf50;
}
.gray {
  background-color: #9e9e9e;
}
</style>