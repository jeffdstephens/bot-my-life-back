<template>
  <h1>Bot My Life Back</h1>
  <div>
    <iframe
      src="https://giphy.com/embed/mIZ9rPeMKefm0"
      width="344"
      height="480"
      frameborder="0"
      class="giphy-embed"
      allowfullscreen
    ></iframe>
  </div>
  <bot-counter />
</template>

<script lang="ts">
import BotCounter from "./components/BotCounter.vue";

export default {
  name: "App",
  components: {
    BotCounter,
  },
};
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
