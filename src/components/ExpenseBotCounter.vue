<template >
  <div class="ExpenseBotCounter">
    <h2>Monthly Cloud Services Expense Report Bot</h2>
    <div>
      <h4>This automation collects billing information from 10 of our AWS cloud instances and creates a single expense report for submission. This bot uses UIPath and is run in attended mode each month. The time it took to complete this task manually was 25 mins. while the attended bot takes 5 mins. for a total personal time savings of 20 mins. per month.</h4>
      <p>
        Start date (the day my bot started doing my expense report for me):
        <b>{{ getStartDate }}</b>
      </p>
      <p>
        Today's date:
        <b>{{ getTodaysDate }}</b>
      </p>
      <p>
        Total number of months elapsed:
        <b>{{ getDayDifferenceAndCalcs() }}</b>
      </p>
      <p>
        Time to complete task (per month):
        <b>{{expenseTaskMinutes}} mins.</b>
      </p>
      <p>
        Total minutes saved:
        <b>{{expenseMinutesElapsed}}</b>
      </p>
      <p>
        Total hours saved:
        <b>{{expenseHoursElapsed }}</b>
      </p>
      <p>
        Total business
        <b>work days saved</b>:
        <b>{{expenseBizDaysSaved }}</b>
      </p>
      <h3>
        Total DAYS I regained of my life!
        {{expenseDaysSaved}}
      </h3>
    </div>
  </div>
</template>

<script>
import { differenceInMonths } from "date-fns/fp";

export default {
  name: "CovidBotCounter",
  props: {},
  data: function () {
    return {
      startDate: new Date(2020, 8, 1),
      todaysDate: new Date(),
      expenseTaskMinutes: 20,
      expenseMinutesElapsed: 0,
      expenseHoursElapsed: 0,
      expenseMonthsElapsed: 0,
      expenseBizDaysSaved: 0,
      expenseDaysSaved: 0,
    };
  },
  computed: {
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
  },
  methods: {
    getDayDifferenceAndCalcs: function () {
      // Get the number of business days - week days - that have elapsed
      var monthDifference = differenceInMonths(this.startDate, this.todaysDate);

      // Subtract the number of OPM stipulated federal holidays during that time
      this.expenseMonthsElapsed = monthDifference;

      // Set the data elements based on the calculated and filtered days
      this.expenseMinutesElapsed =
        this.expenseMonthsElapsed * this.expenseTaskMinutes;
      this.expenseHoursElapsed = (this.expenseMinutesElapsed / 60).toFixed(2);
      this.expenseBizDaysSaved = (this.expenseHoursElapsed / 8).toFixed(2);
      this.expenseDaysSaved = (this.expenseHoursElapsed / 24).toFixed(2);

      return this.expenseMonthsElapsed;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 10px 40px 40px;
}
ul {
  list-style-type: none;
  padding: 0;
}
git branch -m master main li {
  display: inline-block;
  margin: 0 10px;
}
h2 {
  color: #42b983;
}
a {
  color: #42b983;
}
</style>
