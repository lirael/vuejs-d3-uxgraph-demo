<template>
  <div id="app" class="container">
    <div class="row">
      <img class="col-sm-2 col-sm-offset-3" src="./assets/logo.png"> 
      <img class="col-sm-2" src="./assets/d3.png">
      <img class="col-sm-2" src="./assets/ux.png">
    </div>
    <div class="row">
      <router-view></router-view>
    </div>
    <div class="row">
      <p style="float:right">
        Developed by: Olena Pastushenko
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app'
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
</style>
