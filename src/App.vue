<template>
  <h1> TIMERS</h1>
  <button class="addtimerbutton" v-show="!addingNewTimer" @click="setNewTimer"> add a new timer </button>
  <div v-if="addingNewTimer"> 
    <AddTimer :id="idTracking" @set-timer="addNewTimer($event)" @cancel-timer="addingNewTimer=false"/> 
    </div><br>
    <DisplayTimer 
    v-for="(timer, index) in timers" 
    :key="timer.id" 
    :name="timer.name" 
    :time="timer.currentTimerValue"
    @remove-timer="removeTimer(index)"
    @start-timer="startTimer(index)"    
    @pause-timer="stopTimer(timer.timerId)"
    @reset-timer="stopTimer(timer.timerId); timer.currentTimerValue=timer.time; startTimer(index)"
    />

</template>

<script>
import AddTimer from './components/AddTimer.vue'
import DisplayTimer from './components/DisplayTimer.vue'

export default {
  name: 'App',
  components: {
    AddTimer,
    DisplayTimer
  },
  data(){
    return{
      addingNewTimer: false,
      idTracking: 1,
      timers:[],
      timeUp: false
    }
  },
  methods:{
    setNewTimer(){
      this.addingNewTimer = true
    },
    addNewTimer(values){
      this.timers.push({name: values.nameTimer, time: values.time, id: values.id, currentTimerValue: values.time})
      this.addingNewTimer = false
      this.idTracking++
    },

    removeTimer(index){
      if(this.timers[index].timerId){
        this.stopTimer(this.timers[index].timerId)
      }
      this.timers.splice(index, 1)
    },

    startTimer(index){
      this.timers[index].timerId = setInterval(() => {
        if (this.timers[index].currentTimerValue === 0){
          var msg = new SpeechSynthesisUtterance();
          msg.text = this.timers[index].name+" is done";
          window.speechSynthesis.speak(msg);
        }
        this.timers[index].currentTimerValue--
      }, 1000);
    },

    stopTimer(timerId){
      clearInterval(timerId)
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #081d31;
  margin-top: 60px;
}
.addtimerbutton{
  width: 350px;
  text-align: center;
  background: #225a5e;
  color: rgb(255, 255, 255);
  font-weight: bold;
  font-size: 16px;
  border-radius: 10px;
  margin: 5px auto;
  padding: 10px 5px; 
}
</style>
