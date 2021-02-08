<template >
  <div class="BotCounter">
    <h1>{{ msg }}</h1>
    <p>This page represents the time savings I've gained from implementing bots in my life. These bots help me take care of some of the menial tasks so I can do more of the things I love.</p>
  </div>
  <div>
    <h2>COVID-19 Daily Status Report Bot</h2>
    <p>The day my bot started doing my status for me: {{ getStartDate() }}</p>
    <p>Today's date is: {{ getTodaysDate() }}</p>
    <p>Total number of business days since: {{ getDayDifference() }}</p>
  </div>
</template>


<script>
import differenceInBusinessDays from "date-fns/differenceInBusinessDays";

export default {
  name: "BotCounter",
  props: {},
  data: function () {
    return {
      todaysDate: new Date(),
      startDate: new Date("5-19-2020"),
    };
  },
  methods: {
    getStartDate: function () {
      return (
        this.startDate.getMonth() +
        1 +
        "/" +
        this.startDate.getDate() +
        "/" +
        this.startDate.getFullYear()
      );
    },
    getTodaysDate: function () {
      return (
        this.todaysDate.getMonth() +
        1 +
        "/" +
        this.todaysDate.getDate() +
        "/" +
        this.todaysDate.getFullYear()
      );
    },
    getDayDifference: function () {
      return differenceInBusinessDays(this.todaysDate, this.startDate);
    },
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
git branch -m master main li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
