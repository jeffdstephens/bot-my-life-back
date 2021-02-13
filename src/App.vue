<template>
  <div>
    <h1>Bot My Life Back</h1>
    <p>This website shows how I got my life back by implementing bots and automation. These bots help me take care of some of the menial tasks throughout the day so I can do more of the things that I truly love.</p>
  </div>
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
  <covid-bot-counter />
</template>

<script lang="ts">
import CovidBotCounter from "./components/CovidBotCounter.vue";

export default {
  name: "App",
  components: {
    CovidBotCounter,
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
