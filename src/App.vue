<template>
  <div id="app">
    <Header/>
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
import Header from './components/Header.vue'

export default {
  name: 'App',
  components: {
    Calculator,
    Header
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100%;
  text-align: center;
  color: #2c3e50;
  background-color: rgb(34, 12, 87);
}
</style>
