<template>
  <div class="stop-watch-container">
    <div id="time">
      <span class="digit">{{ formatNumber(hours) }}</span>
      <span class="txt">Hr</span>
      <span class="digit">{{ formatNumber(minutes) }}</span>
      <span class="txt">Min</span>
      <span class="digit">{{ formatNumber(seconds) }}</span>
      <span class="txt">Sec</span>
    </div>
    <div class="buttons">
      <button type="button" class="btn btn-success" @click="startStopwatch">
        Start
      </button>
      <button type="button" class="btn btn-danger" @click="stopStopwatch">
        Stop
      </button>
      <button type="button" class="btn btn-warning" @click="resetStopwatch">
        Reset
      </button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
      interval: null,
      isIntervalRunning: false,
    };
  },
  methods: {
    startStopwatch() {
      if (this.isIntervalRunning) {
        return;
      }
      this.isIntervalRunning = true;
      this.interval = setInterval(() => {
        this.seconds++;
        if (this.seconds === 60) {
          this.seconds = 0;
          this.minutes++;
        }
        if (this.minutes === 60) {
          this.minutes = 0;
          this.hours++;
        }
      }, 1000);
    },
    stopStopwatch() {
      this.isIntervalRunning = false;
      clearInterval(this.interval);
    },
    resetStopwatch() {
      this.stopStopwatch();
      this.hours = 0;
      this.minutes = 0;
      this.seconds = 0;
    },
    formatNumber(num) {
      return (num < 10 ? "0" : "") + num;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.stop-watch-container {
  height: 250px;
  width: 500px;
  margin: 0 auto;
  margin-top: 50px;
  background-color: rgb(10, 27, 175);
  border: 1px solid rgb(22, 7, 87);
}
#time {
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  padding: 85px;
}
.txt {
  font-size: 20px;
  padding-top: 30px;
}
.digit {
  font-size: 60px;
}
.buttons {
  position: relative;
  bottom: 60px;
  display: flex;
  justify-content: space-evenly;
}
</style>
