<template>
  <div class="container">
    <div class="clock">
      <div class="hour" :style="{ transform: hourDeg }"></div>
      <div class="minute" :style="{ transform: minuteDeg }"></div>
      <div class="second" :style="{ transform: secondDeg }"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'clock',
  data() {
    return {
      hour: 0,
      minute: 0,
      second: 0,
    }
  },
  computed: {
    hourDeg() {
      let defaultDeg = -90;
      return `rotate(${defaultDeg + 30 * this.hour + 0.5 * this.minute}deg)`;
    },
    minuteDeg() {
      return `rotate(${6 * this.minute + 0.1 * this.second}deg)`;
    },
    secondDeg() {
      let defaultDeg = -180;
      return `rotate(${defaultDeg + 6 * this.second}deg)`;
    },
  },
  created() {
    document.title = '新手 JS 地下城 2F - 時鐘';
    let vm = this;
    setInterval(function() {
      let time = new Date();
      vm.hour = time.getHours();
      vm.minute = time.getMinutes();
      vm.second = time.getSeconds();
    }, 1000);
  },
}
</script>

<style lang="scss">
  .container {
    margin: 0 auto;
    display: flex;
    height: 98vh;
    align-items: center;
    justify-content: center;
  }
  .clock {
    background: url('src/clock-bg.svg');
    width: 500px;
    height: 500px;
    .hour {
      background: url('src/hour-hand.svg');
      width: 72px;
      height: 8px;
      position: absolute;
      top: calc(50% - 4px);
      left: calc(50%);
      transform-origin: left;
      transform: rotate(-90deg);
    }
    .minute {
      background: url('src/minute-hand.svg');
      width: 8px;
      height: 96px;
      position: absolute;
      top: calc(50% - 92px);
      left: calc(50% - 4px);
      transform-origin: 4px 92px;
    }
    .second {
      background: url('src/second-hand.svg') center center no-repeat;
      width: 14px;
      height: 126px;
      position: absolute;
      top: calc(50% + 1px);
      left: calc(50% - 7px);
      transform-origin: top;
      transform: rotate(-180deg);
    }
  }
</style>
