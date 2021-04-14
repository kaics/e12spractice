<template>
  <div>
    <div class="vux-demo" >
      <img class="logo" src="../assets/e12s001.png" style="padding-top: 20px">
      <h1>{{question.text}}</h1>
    </div>
    <div>
      <divider>结果</divider>
    </div>
    <div class="vux-demo" >
      <h1>{{testResult.text}}</h1>
    </div>
    <div class="cellGroup">
      <group title="请选择">
        <cell :title="answer.text" v-for="answer in answerSet" @click.native="testResultWithAnswer(answer)" is-link></cell>
      </group>
    </div>
    <div class="dataExplainBtn" v-on:click="setQuestion">
      <x-button type="primary" action-type="button">测试</x-button>
    </div>

  </div>
</template>

<script>
import { Group, Cell, XButton, Divider } from 'vux'

export default {
  components: {
    Group,
    Cell,
    XButton,
    Divider
  },
  data () {
    return {
      // note: changing this line won't causes changes
      // with hot-reload because the reloaded component
      // preserves its current state and we are modifying
      // its initial state.
      msg: 'Hello World!',
      question:{text: "沙口测试", result: 0},
      testResult:{text: ""},
      questions:[
        {text: '水雷', result: 1},
        {text: '火雷', result: 2},
        {text: '风雷', result: 3},
        {text: '火水', result: 4},
        {text: '风水', result: 5}
      ],
      answers:[
        {text: '外前后', result: 1},
        {text: '外左右', result: 2},
        {text: '外X', result: 3},
        {text: '内左右', result: 4},
        {text: '内X', result: 5}
      ],
      answerSet:[]
    }
  },
  methods: {
    setQuestion() {
      const index = Math.floor(Math.random() * this.questions.length);
      this.question = this.questions[index];
      this.answerSet = this.setRandomAnswer(this.answers);
      this.testResult = {text: ""};
    },
    setRandomAnswer(array) {
      let currentIndex = array.length, temporaryValue, randomIndex;

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {

        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }
      return array;
    },
    testResultWithAnswer(answer) {
      console.log(this.question);
      console.log(answer);
      if (this.question.result == answer.result) {
        this.testResult.text = "还行";
        console.log("correct");
      } else {
        console.log("沙口");
        this.testResult.text = "沙口";
      }

    }
  }
}

</script>

<style>
.vux-demo {
  text-align: center;

  /*position: fixed;*/
}
.logo {
  width: 100px;
  height: 100px
}

/*.btn-button {*/
/*  bottom:10px;*/
/*  position: fixed;*/
/*  left: 50%;*/
/*}*/
#dataExplain {
  position: fixed;
  background-color: white;
}

.cellGroup {
  width: 100%;
  position: absolute;
  bottom: 100px;
  /*transform: translate(6%);*/
}

.dataExplainBtn {
  width: 90%;
  position: absolute;
  bottom: 30px;
  transform: translate(6%);
}

</style>
