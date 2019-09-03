<template>
  <div class="square">
    <h1 v-bind:class="{ hide: (!init && !end) }">{{ msg }}</h1>
    <h1 v-bind:class="{ hide: (init || end) }">Round{{ round + 1 }}</h1>
    <div v-bind:class="{ hide: !init }">
      <p style="color:red;" v-bind:class="{ hide: !invalid }">Name required.</p>
      <div>Name:<br/><input style="font-size:18px;margin-bottom:10px;" v-model="name"></div>
    </div>
    <button v-on:click="start(); startCount()" v-bind:class="{ hide: (!disable || end) }">Start</button>
    <div v-bind:class="{ hide: disable }">
      <h3 v-bind:class="{ hello: test }" style="display:none;">hello</h3>
      <h3 style="display:none">{{ numb }}</h3>
      <table id="table" border="2px solid" align="center">
        <tr>
          <td v-on:click="count(0)" v-bind:class="{ correct: isCorrect[0], wrong: isWrong[ary[0]] }">{{ ary[0] }}</td>
          <td v-on:click="count(1)" v-bind:class="{ correct: isCorrect[1], wrong: isWrong[ary[1]] }">{{ ary[1] }}</td>
          <td v-on:click="count(2)" v-bind:class="{ correct: isCorrect[2], wrong: isWrong[ary[2]] }">{{ ary[2] }}</td>
          <td v-on:click="count(3)" v-bind:class="{ correct: isCorrect[3], wrong: isWrong[ary[3]] }">{{ ary[3] }}</td>
          <td v-on:click="count(4)" v-bind:class="{ correct: isCorrect[4], wrong: isWrong[ary[4]] }">{{ ary[4] }}</td>
        </tr>
        <tr>
          <td v-on:click="count(5)" v-bind:class="{ correct: isCorrect[5], wrong: isWrong[ary[5]] }">{{ ary[5] }}</td>
          <td v-on:click="count(6)" v-bind:class="{ correct: isCorrect[6], wrong: isWrong[ary[6]] }">{{ ary[6] }}</td>
          <td v-on:click="count(7)" v-bind:class="{ correct: isCorrect[7], wrong: isWrong[ary[7]] }">{{ ary[7] }}</td>
          <td v-on:click="count(8)" v-bind:class="{ correct: isCorrect[8], wrong: isWrong[ary[8]] }">{{ ary[8] }}</td>
          <td v-on:click="count(9)" v-bind:class="{ correct: isCorrect[9], wrong: isWrong[ary[9]] }">{{ ary[9] }}</td>
        </tr>
        <tr>
          <td v-on:click="count(10)" v-bind:class="{ correct: isCorrect[10], wrong: isWrong[ary[10]] }">{{ ary[10] }}</td>
          <td v-on:click="count(11)" v-bind:class="{ correct: isCorrect[11], wrong: isWrong[ary[11]] }">{{ ary[11] }}</td>
          <td v-on:click="count(12)" v-bind:class="{ correct: isCorrect[12], wrong: isWrong[ary[12]] }">{{ ary[12] }}</td>
          <td v-on:click="count(13)" v-bind:class="{ correct: isCorrect[13], wrong: isWrong[ary[13]] }">{{ ary[13] }}</td>
          <td v-on:click="count(14)" v-bind:class="{ correct: isCorrect[14], wrong: isWrong[ary[14]] }">{{ ary[14] }}</td>
        </tr>
        <tr>
          <td v-on:click="count(15)" v-bind:class="{ correct: isCorrect[15], wrong: isWrong[ary[15]] }">{{ ary[15] }}</td>
          <td v-on:click="count(16)" v-bind:class="{ correct: isCorrect[16], wrong: isWrong[ary[16]] }">{{ ary[16] }}</td>
          <td v-on:click="count(17)" v-bind:class="{ correct: isCorrect[17], wrong: isWrong[ary[17]] }">{{ ary[17] }}</td>
          <td v-on:click="count(18)" v-bind:class="{ correct: isCorrect[18], wrong: isWrong[ary[18]] }">{{ ary[18] }}</td>
          <td v-on:click="count(19)" v-bind:class="{ correct: isCorrect[19], wrong: isWrong[ary[19]] }">{{ ary[19] }}</td>
        </tr>
        <tr>
          <td v-on:click="count(20)" v-bind:class="{ correct: isCorrect[20], wrong: isWrong[ary[20]] }">{{ ary[20] }}</td>
          <td v-on:click="count(21)" v-bind:class="{ correct: isCorrect[21], wrong: isWrong[ary[21]] }">{{ ary[21] }}</td>
          <td v-on:click="count(22)" v-bind:class="{ correct: isCorrect[22], wrong: isWrong[ary[22]] }">{{ ary[22] }}</td>
          <td v-on:click="count(23)" v-bind:class="{ correct: isCorrect[23], wrong: isWrong[ary[23]] }">{{ ary[23] }}</td>
          <td v-on:click="count(24)" v-bind:class="{ correct: isCorrect[24], wrong: isWrong[ary[24]] }">{{ ary[24] }}</td>
        </tr>
      </table>
      <h3>Touch {{ counter + 1 }}</h3>
      <div>Time: {{ formatTime }}sec</div>
      <h3>{{ mistakes }} mistakes</h3>
    </div>
    <div v-bind:class="{ hide: init }" style="margin-top:10px;">Name: {{ name }}</div>
    <ul style="list-style: none;">
      <li v-bind:class="{ hide: !roundResult[0] }">
        <span>Round1  </span>
        <span>Time: {{ Math.round(resultTime[0] * 10) / 10 }}sec  </span>
        <span>Mistakes: {{ resultMistakes[0] }}  </span>
        <span>Ratio: {{ Math.round(((25 - resultMistakes[0]) / 25) * 10000) / 100 }}%</span>
      </li>
      <li v-bind:class="{ hide: !roundResult[1] }">
        <span>Round2  </span>
        <span>Time: {{ Math.round(resultTime[1] * 10) / 10 }}sec  </span>
        <span>Mistakes: {{ resultMistakes[1] }}  </span>
        <span>Ratio: {{ Math.round(((25 - resultMistakes[1]) / 25) * 10000) / 100 }}%</span>
      </li>
      <li v-bind:class="{ hide: !roundResult[2] }">
        <span>Round3  </span>
        <span>Time: {{ Math.round(resultTime[2] * 10) / 10 }}sec  </span>
        <span>Mistakes: {{ resultMistakes[2] }}  </span>
        <span>Ratio: {{ Math.round(((25 - resultMistakes[2]) / 25) * 10000) / 100 }}%</span>
      </li>
      <li v-bind:class="{ hide: !roundResult[2] }">
        <span>Total  &nbsp;&nbsp;&nbsp;&nbsp;</span>
        <span>Time: {{ Math.round(sum(resultTime) * 10) / 10 }}sec  </span>
        <span>Mistakes: {{ sum(resultMistakes) }}  </span>
        <span>Ratio: {{ Math.round(((245 - sum(resultMistakes)) / 245) * 10000) / 100 }}%</span>
      </li>
    </ul>
  </div>
</template>
<script>
    import _ from 'lodash'
    export default {
    name: 'Square',
    props: {
        msg: String,
    },
    data () {
        const top = [1]
        const middle = _.shuffle(Array.from(Array(23).keys(), x => x + 2))
        const bottom = [25]
        return {
        name: null,
        init: true,
        invalid: false,
        ary: top.concat(middle).concat(bottom),
        counter: 0,
        isCorrect: new Array(25).fill(false),
        isWrong: new Array(25).fill(false),
        test: false,
        numb: 1,
        mistakes: 0,
        startTime: null,
        time: null,
        round: 0,
        resultTime: new Array(3).fill(null),
        resultMistakes: new Array(3).fill(null),
        roundResult: new Array(3).fill(false),
        disable: true,
        end: false,
        api_result: null,
        min: 0,
        sec: 0,
        smallSec: 0,
        timerOn: false,
        timerObj: null,
        timeNow: 0
        }
    },
    computed: {
        formatTime: function() {
        var formattedTime = this.timeNow.toFixed(1)
        return formattedTime
        }
    },
    methods: {
        count: function(selected) {
        this.test = true
        if (this.ary[selected] == (this.counter + 1)) {
            this.counter += 1
            this.isCorrect[selected] = true
        } else {
            this.isWrong[this.counter + 1] = true
            this.numb = this.counter + 1
            this.mistakes += 1
        }
        if (this.counter == 25) {
            clearInterval(this.timerObj)
            this.sec = 0
            this.min = 0
            this.timerOn = false
            this.isCorrect.fill(false)
            this.isWrong.fill(false)
            this.time = (new Date() - this.startTime) / 1000
            this.disable = !this.disable
            this.resultTime[this.round] = this.time
            this.resultMistakes[this.round] = this.mistakes
            this.roundResult[this.round] = true
            this.round += 1
            if (this.round > 2) {
            this.end = true
            }
            this.counter = 0
            this.startTime = null
            this.time = null
            this.mistakes = 0
            const top = [1]
            const middle = _.shuffle(Array.from(Array(23).keys(), x => x + 2))
            const bottom = [25]
            this.ary = top.concat(middle).concat(bottom)
        }
        },
        countTime: function() {
        this.timeNow = (new Date() - this.startTime) / 1000
        },
        startCount: function() {
        let self = this;
        this.timerObj = setInterval(function() {self.countTime()}, 10)
        this.timerOn = true;
        },
        start: function() {
        if (this.init && (this.name == null) || (this.name == "")) {
            this.invalid = true
        } else {
            if (this.init) {
            this.init = false
            }
            this.disable = !this.disable
            this.startTime = new Date()
        }
        },
        sum: function(arr) {
        return arr.reduce(function(prev, current) {
            return prev+current;
        });
        }
    }
    }
</script>
<style scoped>
  #table {
    width: 20em;
    margin-bottom: 1em;
  }
  td {
    height: 3.6em;
  }
  .wrong {
    background-color: fuchsia;
  }
  .correct {
    background-color: lightgreen;
  }
  .hello {
    color: red;
  }
  .hide {
    display: none;
  }
</style>