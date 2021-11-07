<template >
  <div class="ExpenseBotCounter">
    <h2>Monthly Cloud Services Expense Report Bot</h2>
    <div>
      <h4>This automation collects billing information from 10 of our AWS cloud instances and creates a single expense report for submission.</h4>
      <h4>This bot uses UIPath and is run in attended mode each month. The time it took to complete this task manually was 25 mins. while the attended bot takes 5 mins. for a total personal time savings of 20 mins. per month.</h4>

      <hr />

      <div class="flex-details-container">
        <div class="flex-label">Start date (the day my bot started doing my expense report for me):</div>
        <div class="flex-value">
          <b>{{ getStartDate }}</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Today's date:</div>
        <div class="flex-value">
          <b>{{ getTodaysDate }}</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Total number of months elapsed:</div>
        <div class="flex-value">
          <b>{{ getDayDifferenceAndCalcs() }} months</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Time to complete task (per month):</div>
        <div class="flex-value">
          <b>{{expenseTaskMinutes}} mins.</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Total minutes saved:</div>
        <div class="flex-value">
          <b>{{expenseMinutesElapsed}} mins.</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Total hours saved:</div>
        <div class="flex-value">
          <b>{{expenseHoursElapsed }} hrs.</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">
          Total business
          <b>work days saved</b>:
        </div>
        <div class="flex-value">
          <b style="color:red;">{{expenseBizDaysSaved }} days</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">
          <b>Total DAYS I regained of my life!</b>
        </div>
        <div class="flex-value">
          <b style="color:red;">{{expenseDaysSaved}} days!</b>
        </div>
      </div>
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
