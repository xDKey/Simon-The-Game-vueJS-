<template>
  <div id="app">
    <h1>Simon The Game</h1>
    <div class='gameField'>
      <Square 
       :props="{
        id: 'r',
        color: 'red'
      }"
       @choise='this.choise'/>      

      <Square 
       :props="{
        id: 'g',
        color: 'green'
      }"
       @choise='this.choise'/>      
      
      <Square 
       :props="{
        id: 'b',
        color: 'blue'
      }"
       @choise='this.choise'/>      
      
      <Square 
       :props="{
        id: 'y',
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
    check(){
      console.log(this)
    },
    choise(id){
      console.log(id)
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
</style>