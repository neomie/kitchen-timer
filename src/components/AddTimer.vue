<template>
<div class="backdrop">
<div class="addtimer">
  <form>
    <label class="labelnametimer">name of the timer:</label>
    <input class="inputtext" type="text" v-model="nameTimer">
    <label>minutes: </label>
    <input class="inputnumber" type="number" min=0 v-model="minutes">

    <label>seconds: </label>
    <input class="inputnumber" type="number" min=0 max=59 v-model="seconds">
 </form>
 <button class="settimerbutton" @click="addTimer"> add the timer </button>
 <button class="settimerbutton" @click="cancel">cancel</button>
</div>
</div>
</template>

<script>
export default {
    props:{ 
        id: Number
        },
    data(){
        return{
            nameTimer: '',
            minutes: 0,
            seconds: 0
        }
    },
    emits:['set-timer', 'cancel-timer'],
    methods:{
        addTimer(){
            if(!this.nameTimer){this.nameTimer='Timer '+this.id}
            var time = this.seconds+this.minutes*60
            if(time<1){
              alert("please set a time")
                return
            }
            this.$emit('set-timer', {nameTimer: this.nameTimer, time: time, id: this.id})
        },
        cancel(){
            this.$emit('cancel-timer')
        }
    }
}
</script>

<style >
.addtimer {
  position: fixed;
  top: 35%;
  left: 35%;
  margin: 10px auto ;
  padding: 15px ;
  width: 30%;
  border-radius: 10px;
  text-align: center;
  background: #ccd9db;
  color: black;
}
  label {
    color: rgb(5, 31, 34);
    margin: 20px 10px ;
    font-size: 20;
    font-weight: bold;
  }

  .inputtext {
    padding: 10px 6px;
    width: 90%;
    margin: 5px 5px 5px;
    box-sizing:border-box;
    border: none;
    color: #555;
  }
  .inputnumber {
    padding: 10px 6px;
    margin: 10px 10px 10px;
    width: 15%;
    box-sizing:border-box;
    border: none;
    color: #555;
  }
.settimerbutton{
    text-align: center;
    background: #344f55;
    color: rgb(255, 255, 255);
    font-size: 16px;
    border-radius: 5px;
  }
  .backdrop{
      top: 0;
      position: fixed;
      background: rgba(0,0,0,0.5);
      width: 100%;
      height: 100%;
  }
</style>