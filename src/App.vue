<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <button v-on:click="addEntity()">+ Add Entity</button>

    <div class="entity-list">
      <Entity v-for="(item, index) in entities" v-bind:key="index"/>
    </div> 
  </div>
</template>

<script>
import Entity from './components/Entity.vue'

export default {
  name: 'app',
  components: {
    Entity
  },
  data: () => {
    return {
      entities: [{}]
    }
  },
  methods: {
    addEntity() {
      this.entities.push({})
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  margin-top: 60px;
}
.entity-list {
display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
}
</style>
