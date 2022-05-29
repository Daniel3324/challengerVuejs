<template>
  <div id="app">
    <BuildForm msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import BuildForm from './components/BuildForm.vue'

export default {
  name: 'App',
  components: {
    BuildForm
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
}
</style>
