<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="The simple Vue Caculator"/>
    <Caculator/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Caculator from './components/Caculator.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Caculator
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
</style>
