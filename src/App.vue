<template>
  <div id="app">
    <h1>Simon The Game</h1>
    <button class='startButton'
    @click='this.startGame'>Start Game</button>
    <div class='gameField'>
      <Square 
       :props="{
        id: '1',
        color: 'red'
      }"
       @choise='this.choise'/>      

      <Square 
       :props="{
        id: '2',
        color: 'green'
      }"
       @choise='this.choise'/>      
      
      <Square 
       :props="{
        id: '3',
        color: 'blue'
      }"
       @choise='this.choise'/>      
      
      <Square 
       :props="{
        id: '4',
        color: 'yellow'
      }"
       @choise='this.choise'/>

    </div>
  </div>
</template>

<script>
import Square from './components/Square';

export default {
  name: 'App',
  data() {
    return{
      computer: [],
      player: [],
    }
  },
  components:{
    Square,
  },
  methods:{
    choise(id){
      console.log(id)
    },
    startGame(){
      this.computer = [];
      this.player = [];
      this.round();
    },
    round(){
      let round = 0;
      let idx = Math.floor(Math.random() * (5 - 1) + 1);
      this.computer.push(idx);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #2c3e50;
  margin-top: 60px;
}
.gameField{
  width: 250px;
  height: 250px;
  display: flex;
  flex-wrap: wrap;
}
.startButton{
    background-color: #4CAF50;
    border: none;
    border-radius: 50%;
    color: white;
    padding: 15px 32px;
    text-align: center;
    display: inline-block;
    margin: 4px 2px;
    cursor: pointer;
}
</style>