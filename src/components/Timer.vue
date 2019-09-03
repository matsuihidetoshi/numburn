<template>
  <div id="timer">
    <div class="timer">
      <div class="time">
        {{ formatTime }}
      </div>
      <button v-on:click="start" v-if="!timerOn">Start</button>
      <button v-on:click="stop" v-if="timerOn">Stop</button>
    </div>
  </div>
</template>

<script>
    export default {
    name: 'Timer',
    data() {
        return {
        min: 0,
        sec: 0,
        timerOn: false,
        timerObj: null,
        }
    },
    methods: {
        count: function() {
        if (this.sec < 59){
            this.sec += 1
        } else {
            this.sec = 0
            if (this.min < 59){
            this.min += 1
            } else {
            this.min = 0
            }        
        }
        },
        start: function() {
        let self = this;
        this.timerObj = setInterval(function() {self.count()}, 1)
        this.timerOn = true; //timerがOFFであることを状態として保持
        },
        stop: function() {
        clearInterval(this.timerObj);
        this.timerOn = false; //timerがOFFであることを状態として保持
        },
        complete: function() {
        clearInterval(this.timerObj)
        }
    },
    computed: {
        formatTime: function() {
        let timeStrings = [
            this.min.toString(),
            this.sec.toString()
        ].map(function(str) {
            if (str.length < 2) {
            return "0" + str
            } else {
            return str
            }
        })
        return timeStrings[0] + ":" + timeStrings[1]
        }
    }
    }
</script>

<style scoped>
    #timer {
    display: flex;
    align-items: center;
    justify-content: center;
    }
    .time {
    font-size: 100px;
    }
</style>