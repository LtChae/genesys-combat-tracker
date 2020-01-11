<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <Entity/>
  </div>
</template>

<script>
import Entity from './components/Entity.vue'

export default {
  name: 'app',
  components: {
    Entity
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  justify-content: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
