<template>
  <div>
    <div id="computer" :style="computedStyleObject"></div>
    <div>
      <button @click="onClickButton('바위')">바위</button>
      <button @click="onClickButton('가위')">가위</button>
      <button @click="onClickButton('보')">보</button>
    </div>
    <div>{{ result }}</div>
    <div>현재 {{ score }}점</div>
    <lifecycle-example v-if="true" />
  </div>
</template>

<script>
const rspCoords = {
  바위: '0',
  가위: '-142px',
  보: '-284px',
};

const scores = {
  가위: 1,
  바위: 0,
  보: -1
};

const computerChoice = (imgCoord) => {
  return Object.entries(rspCoords).find(function (v) {
    return v[1] === imgCoord;
  })[0];
};

let interval = null;
export default {
  data() {
    return {
      imgCoord: rspCoords.바위,
      result: '',
      score: 0,
    }
  },
  computed: {
    computedStyleObject() {
      return { background: `url(https://en.pimg.jp/023/182/267/1/23182267.jpg) ${this.imgCoord} 0` };
    }
  },
  methods: {
    changeHand() {
      interval = setInterval(() => {
        if (this.imgCoord ===  rspCoords.바위) {
          this.imgCoord = rspCoords.가위;
        } else if (this.imgCoord === rspCoords.가위) {
          this.imgCoord = rspCoords.보;
        } else if (this.imgCoord === rspCoords.보) {
          this.imgCoord = rspCoords.바위;
        }
      }, 100);
    },
    onClickButton(choice) {
      clearInterval(interval);
      const myScore = scores[choice];
      const cpuScore = scores[computerChoice(this.imgCoord)];
      const diff = myScore - cpuScore;
      if (diff === 0) {
        this.result = '비김~';
      } else if ([-1, 2].includes(diff)) {
        this.result = '이김~'
        this.score += 1;
      } else {
        this.result = '짐ㅠ';
        this.score -= 1;
      }
      setTimeout(() => {
        this.changeHand();
      }, 1000);
    },
  },
  created() {
    console.log('created');
  },
  mounted() {
    console.log('mounted');
    this.changeHand();
  },
  updated() {
    // console.log('updated');
  },
  beforeDestroy() {
    clearInterval(interval);
  },
  destroyed() {
    // console.log('destroyed');
  },
};
</script>

<style scoped>
  #computer {
    width: 142px;
    height: 200px;
    background-position: 0 0;
  }
</style>