<template>
  <h1>Reaction time test</h1>
  <p>Press the start button and when the red box appears click on it as fast as you can</p>
  
  <button class="button" @click="startGame">Start</button>
  <div @click.self="borderClicked()" class="border"> 
    <div v-if="showBox" class="box" @click="userTrigger"></div>
  </div>
  <div v-if="showResult" class="Result">{{displayScore()}}</div> 
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      showBox: false,
      startTime: null,
      endTime: null,
      showResult: false,
      gameStarted: false
    }
  },
  methods: {
    toggleBox() {
      this.showBox = !this.showBox
    },
    startGame() {
      this.gameStarted = true
      this.showResult = false
      setTimeout(()=>{
        this.toggleBox()
        this.startTime = Date.now()
      }, 800 + Math.random()*4000 )
    },
    userTrigger() {
      this.endTime = Date.now()
      this.showBox = false
      this.showResult = true
      this.gameStarted = false
    },
    displayScore() {
      return this.endTime - this.startTime + " ms"
    },
    borderClicked() {
      if(this.gameStarted) {
        alert("jump start")
        this.reset()
      }
    },
    reset() {
      this.showBox = false,
      this.startTime = null,
      this.endTime = null,
      this.showResult = false,
      this.gameStarted = false
    }
    
  }
}
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
.box {
  background: blue;
  width: 20rem;
  height: 20rem;
  margin: auto;
}
.button {
  background-color: #04AA6D; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
.border {
  border: 1px solid #2c3e50;
  height: 20rem;
  width: 20rem;
  margin: auto;
}
</style>
