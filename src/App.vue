<template>
  <div id="app">
    <!-- <img width="25%" src="./assets/logo.png"> -->
    <Azul/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Azul from './components/Azul';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Azul,
  },
};
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
