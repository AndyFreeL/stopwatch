<template>
  <div class = 'wrapper'>
    <div v-for = 'i in count'><StopWatch></StopWatch></div>
    <div class="addBtn" @click="addTimer(+1)">+</div>
  </div>
</template>

<script>
import StopWatch from "./StopWatch.vue";
export default {
  name: "StopWatchList",
  components: {StopWatch},
  data () {
    return {
      count:1,
    }
  },
  methods:{
    addTimer(change) {
      this.count = Math.max(0, Math.min(12, this.count + change));
    },
  }
}
</script>

<style scoped>
.wrapper{
  display: flex;
  flex-wrap: wrap;
}
.addBtn{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 40px;
  width: 225px;
  height: 120px;
  background: #696969;
  cursor: pointer;
  margin: 22.5px 25px;
  color: #9E9E9E;
}
</style>