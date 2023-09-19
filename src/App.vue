<template>
  <div :class="{ blueColor: gameStop, greenColor: gameStart }">
    <GoButton @start="go" @stop="stop" />
    <ResultDisplay :message="Resultmessage" :highscore="highscore" />
  </div>
</template>

<script>

import GoButton from './components/Gobutton.vue'
import ResultDisplay from './components/Result.vue'

export default {
  name: 'App',
  data() {
    return {
      gameStop: true,
      gameStart: false,
      interval: null,
      Resultmessage: 'Click go to your reaction time',
      startTime: null,
      formattedTime: '',
      highscore: 'N/A'
    }
  },
  components: {
    GoButton,
    ResultDisplay
  },
  methods: {
    go() {
      this.interval = setTimeout(() => {
        this.gameStop = false;
        this.gameStart = true;
        this.startTime = Date.now();
      }, 3000);
      this.Resultmessage = "Pay attention. Click stop when the color changes"
    },


    stop() {
      this.gameStop = true
      clearInterval(this.interval);
      if (this.gameStart) {
        const endTime = Date.now();
        const reactionTime = (endTime - this.startTime) / 1000;
        this.formattedTime = reactionTime.toFixed(2) + ' sec';
      } else {
        this.formattedTime = 'N/A';
      }
      this.Resultmessage = this.greenVisible ?  `Your time was: ${this.formattedTime}. Try again! ` : "Too quick... Try again!"
      if (this.formattedTime && (this.highscore > this.formattedTime)) {
        this.Resultmessage = `You've set a new high score: ${this.formattedTime}`
        this.highscore = this.formattedTime
      }
      this.gameStart = false
      clearInterval(this.startTime);
      clearInterval(this.formattedTime);
    }
  }
}
</script>

<style >
* {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}

.greenColor {
  width: 100%;
  height: 100vh;
  background-color: rgb(32, 146, 40);
}

.blueColor {
  width: 100%;
  height: 100vh;
  background-color: rgb(32, 34, 146);
}
</style>
