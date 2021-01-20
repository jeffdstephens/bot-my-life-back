<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <bot-counter msg="Bot My Life Back"/>
</template>

<script lang="ts">
import BotCounter from './components/BotCounter.vue'

export default {
  name: 'App',
  components: {
    BotCounter
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
