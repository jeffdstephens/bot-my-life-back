<template>
  <div>
    <div>
      <h1>Bot My Life Back</h1>
      <h7>
        human:
        <a href="https://www.jeffdstephens.com" target="_blank">jeffdstephens</a>
      </h7>
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

    <div class="flex-container">
      <covid-bot-counter class="flex-item" />
      <expense-bot-counter class="flex-item" />
    </div>
  </div>
</template>

<script lang="ts">
import CovidBotCounter from "./components/CovidBotCounter.vue";
import ExpenseBotCounter from "./components/ExpenseBotCounter.vue";

export default {
  name: "App",
  components: {
    CovidBotCounter,
    ExpenseBotCounter,
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
  margin-top: 20px;
  margin-left: auto;
  margin-right: auto;
  max-width: 1080px;
}

.flex-container {
  display: flex;
  padding: 20px;
  flex-direction: row;
  justify-content: space-around;
}

.flex-item {
  flex: 1;
  padding: 1.5em;
  margin: 1em;
  text-align: center;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

/* Responsive layout - makes a one column layout instead of a two-column layout */
@media (max-width: 800px) {
  .flex-container {
    flex-direction: column;
  }
}

h4 {
  text-align: left;
}

.flex-details-container {
  display: flex;
  padding: 0;
  flex-direction: row;
}

.flex-label {
  flex: 2;
  text-align: left;
  padding: 0.5em;
}

.flex-value {
  flex: 1;
  text-align: right;
  padding: 0.5em;
}

.summary-hr {
  border-top: 5px solid #8c8b8b;
}
</style>
