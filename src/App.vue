<template>
  <div id="app">
    <a href="https://github.com/corey-v">
      <img src="./assets/github_icon.png">
    </a>
    <a href="https://www.goldeneagleweb.ca">
      <img src="./assets/gew_icon.png">
    </a>
    <a href="https://www.linkedin.com/in/corey-valentyne">
      <img src="./assets/new_linkedin_icon.png">
    </a>
    <br>
    <img src="./assets/logo.png">

    <Calculator/>
  </div>

</template>

<script>
import Calculator from './components/Calculator'

export default {
  name: 'app',
  components: {
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
