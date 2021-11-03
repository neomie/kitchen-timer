<template>
  <div class="timer" v-if="time>0"> 
      <h2>{{name}}</h2>
      {{minutes}} minutes and 
      {{seconds}} seconds left   
      <br>
    <button v-if="!timerRunning" class="timerbutton" @click="startTimer"> Start</button>
    <button v-else class="timerbutton" @click="pauseTimer"> Pause </button>
    <button class="timerbutton" @click="removeTimer"> Remove </button>
  </div>
  <div class="timer-finished" v-else>
    <h2> {{name}} is done!</h2>
    <br>
    <button class="timerbutton" @click="restartTimer"> Reset</button> 
    <button class="timerbutton" @click="removeTimer"> Remove </button>
  </div>
</template>

<script>
export default {
    name: 'DisplayTimer',
    props: {
        name: String,
        time: Number
    },
    emits: ['remove-timer', 'start-timer', 'pause-timer', 'reset-timer'],
    data(){
      return{
        timerRunning: false
        }
    },
    methods: {
      startTimer(){
        this.timerRunning=true
        this.$emit('start-timer')
      },
      pauseTimer(){
        this.timerRunning=false
        this.$emit('pause-timer')
      },
      removeTimer(){
        this.$emit('remove-timer')
      },
      restartTimer(){
        this.timerRunning=true
        this.$emit('reset-timer')
      }
    },
    computed:{
      minutes: function(){
        var minutes = Math.floor(this.time/60)
        return minutes
      },
      seconds: function(){
        var seconds = this.time-this.minutes*60
        return seconds
      }
    }
}
</script>

<style >
.timer {
  height: 120px;
  width: 300px;
  border-radius: 10px;
  background: #c2ccce;
  color: black;
  text-align: center;
  margin: 10px 5px ;
  padding: 5px 5px ;
  font-weight: bold;
  border: solid;
  border-color: #708286 ;
  display: inline-block;
}
.timer-finished {
  height: 120px;
  width: 300px;
  border-radius: 10px;
  background: #334246;
  color: rgb(255, 255, 255);
  text-align: center;
  margin: 10px ;
  padding: 5px 0;
  font-weight: bold;
  border: solid;
  border-color: #708286 ;
  display: inline-block;
}
button{
  margin: 5px;
  padding: 5px 5px; 
}

</style>