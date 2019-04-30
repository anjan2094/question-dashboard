<template>
  <div id="app">
     <h1 class="dash-title">Dashboard</h1>
     <Api />
  </div>
</template>

<script>
import Api from './components/Api';
export default {
  name: 'app',
  components: {
    Api
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
body, html{
  margin: 0;
  padding: 0;
}
.dash-title{
  margin-top: -1px;
  text-align: center;
  font-size: 3em;
  color: azure;
  background-color: darkslateblue;
}
</style>
