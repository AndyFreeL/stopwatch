<template>
<div class="stopWatch" v-bind:class="{active:timerState==='running'}">
  <div class="blk countBlk">
    <div class="timer">{{formattedTime}}</div>
  </div>
  <div class="blk">
    <div class='btnBlk'>
      <div v-if="timerState!=='running' " class=" play timerBtn" @click='start'></div>
      <div v-else class="pause timerBtn" @click='pause'></div>
      <div class="stop timerBtn" @click='stop'></div>
    </div>
  </div>
</div>
</template>

<script>
export default{
  name: "StopWatch",
  data () {
    return {
      timerState: 'stopped',
      currentTimer: 0,
      formattedTime: "00",
      ticker: undefined,
      snackbar: false
    }
  },
  methods: {

    start () {
      if (this.timerState !== 'running') {
        this.tick();
        this.timerState = 'running';
      }
    },
    pause () {
      window.clearInterval(this.ticker);
      this.timerState = 'paused';
    },
    stop () {
      window.clearInterval(this.ticker)
      this.currentTimer = 0;
      this.formattedTime = "00";
      this.timerState = "stopped";
    },
    tick () {
      this.ticker = setInterval(() => {
        this.currentTimer++;
        this.formattedTime = this.formatTime(this.currentTimer);
      }, 10)
    },
    formatTime (seconds) {
      let measuredTime = new Date(null);
      measuredTime.setSeconds(seconds);
      let MHSTime = measuredTime.toISOString().substr(11, 8);

      if(MHSTime.substring(0,5)==='00:00'){
        return MHSTime.substring(6,8)
      }else if(MHSTime.substring(0,2)==='00'){
        return MHSTime.substring(3,8)
      }else{
        return MHSTime
      }
    }
  }
}
</script>

<style>
:root {
  --color-primary: #9E9E9E;
}
.stopWatch{
  margin: 22.5px 25px;
  width: 225px;
  background: #696969;
  display: flex;
  flex-direction: column;
  color: var(--color-primary);
}
.blk{
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.countBlk{
  border-bottom: 1px solid var(--color-primary);
  font-size: 22px;
  line-height: 21.05px;
}
.timerBtn{
  cursor: pointer;
}
.btnBlk{
  display: flex;
  width: 88px;
  justify-content: space-between;
}
.play{
  box-sizing: border-box;
  width: 20px;
  height: 20px;
  position: relative;
}
.play:before {
   display: block;
   content: "";
   position: absolute;
   border-top: 10px solid transparent;
   border-bottom:10px solid transparent;
   border-left: 17px solid var(--color-primary);
 }
.pause{
  box-sizing: border-box;
  width: 10px;
  height:20px;
  position: relative;
}
.pause:before, .pause:after{
  display: block;
  width: 3px;
  content: "";
  background:var(--color-primary);
  height: 100%;
  position: absolute;
}
.pause:before{
  left: 0;
  top: 0;
}
.pause:after{
  right: 0;
  top: 0;
}
.stop{
  width: 20px;
  height: 20px;
  background: var(--color-primary);
}
.active{
--color-primary:white;
}


</style>
