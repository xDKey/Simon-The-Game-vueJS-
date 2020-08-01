<template>
  <div id="app">
    <h1>Simon The Game</h1>
    <button class='startButton'
    @click='this.startGame'>{{this.buttonText}}</button>
    <div class='gameField'>
      <Square 
       :props="{
        id: '1',
        color: 'red'
      }"
       @choise='this.choise'
       :class='{bigger: isBigger[1]}'/>      

      <Square 
       :props="{
        id: '2',
        color: 'green'
      }"
       @choise='this.choise'
       :class='{bigger: isBigger[2]}'/>      
      
      <Square 
       :props="{
        id: '3',
        color: 'blue'
      }"
       @choise='this.choise'
       :class='{bigger: isBigger[3]}'/>      
      
      <Square 
       :props="{
        id: '4',
        color: 'yellow'
      }"
       @choise='this.choise'
       :class='{bigger: isBigger[4]}'/>

    </div>
    <span>Scores: {{this.score}}</span>
      <form>Difficult:
      <label>
        <input name='dif' type='radio' value='1500' v-model='difficult'> Easy
      </label>
      <label>
        <input name='dif' type='radio' value='1000' v-model='difficult'> Normal
      </label>
      <label>
        <input name='dif' type='radio' value='450' v-model='difficult'> Hard
      </label>
    </form>
  </div>
</template>

<script>
import Square from './components/Square';

export default {
  name: 'App',
  data() {
    return{
      buttonText: 'Start Game',
      difficult: 1000,
      playing: false,
      computer: [],
      player: [],
      isClickable: false,
      interval: null,
      score: 0,
      sounds: [
       new Audio(require('./assets/1.mp3')),
       new Audio(require('./assets/2.mp3')),
       new Audio(require('./assets/3.mp3')),
       new Audio(require('./assets/4.mp3')),
      ],    
      isBigger: {
        1: false,
        2: false,
        3: false,
        4: false,
      }
    }
  },
  components:{
    Square,
  },
  methods:{
    choise(id){
      if (this.isClickable){
        this.player.push(id);
        this.bigger(id);
        this.playSound(id);
        this.isWinner()
      }
    },
    playSound(id){
        this.sounds[id-1].play();
    },
    bigger(id){
      this.isBigger[id] = true;
      setTimeout(() => {this.isBigger[id] = false}, 300)
    },
    isWinner(){
      for (let i = 0; i < this.player.length; i++){
        if (this.player[i] != this.computer[i]) {
          this.isClickable = false;
          this.buttonText = 'You Lose! Play again?';
          return null
        }
        if (this.player.length == this.computer.length) {
          this.player = [];
          this.score++;
          setTimeout(() => {this.round()}, 1000);
        }
      }
    },
    startGame(){
      this.playing = true;
      this.computer = [];
      this.player = [];
      this.score = 0;
      this.buttonText = 'Reset';
      clearInterval(this.interval);
      this.round();
    },
    round(){
      let round = 0;
      let speed = this.computer.length == 0 ? 1000 : this.difficult;
      this.isClickable = false;
      let idx = Math.floor(Math.random() * (5 - 1) + 1);
      this.computer.push(idx);
      this.interval = setInterval(() => {
        if(round >= this.computer.length){
          clearInterval(this.interval);
          return (this.isClickable = true);
        }
        this.bigger(this.computer[round]);
        this.playSound(this.computer[round]);
        round++;
      }, speed ) 

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
.bigger{
  transform: scale(1.2);
}
</style>