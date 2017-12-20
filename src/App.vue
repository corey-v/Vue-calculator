<template>
  <div id="app">
    <img src="./assets/logo.png">
   
    <Calculator/>
  </div>

</template>

<script>
import HelloWorld from './components/HelloWorld'
import Calculator from './components/Calculator'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Calculator
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
  background: linear-gradient(to bottom, darkgreen, lightgreen) no-repeat;
}
</style>
