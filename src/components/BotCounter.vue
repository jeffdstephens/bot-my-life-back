<template >
  <div class="BotCounter">
    <h1>{{ msg }}</h1>
    <p>This page represents the time savings I've gained from implementing bots in my life. These bots help me take care of some of the menial tasks so I can do more of the things I love.</p>
  </div>
</template>

<script>
export default {
  name: "BotCounter",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
