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
        <div class="flex-label">Minutes saved:</div>
        <div class="flex-value">
          <b>{{expenseMinutesElapsed}} mins.</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Hours saved:</div>
        <div class="flex-value">
          <b>{{expenseHoursElapsed }} hrs.</b>
        </div>
      </div>

      <hr />

      <div class="flex-details-container">
        <div class="flex-label">
          In December 2021 I decided to finish the rest of the automation by having the bot login to our online system, fill out a new expense report, attach the file, and have it saved and ready for me to manually submit (after a quick check of course). This additional automation saved me the final 5 minutes of the process and is added into the final numbers below.
          <br />
          <br />By the way, if you are interested in learning how you can integrate UIPath with GitLab, be sure to check out
          <a
            href="https://www.jeffdstephens.com/how-to-integrate-uipath-with-gitlab/"
            target="_blank"
          >my blog post</a> and video where I walk you through the process.
        </div>
      </div>

      <hr />

      <div class="flex-details-container">
        <div class="flex-label">Start date of phase 2:</div>
        <div class="flex-value">
          <b>{{ getPhase2StartDate }}</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Time to complete additional tasks (per month):</div>
        <div class="flex-value">
          <b>{{phase2ExpenseTaskMinutes}} mins.</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Additional minutes saved:</div>
        <div class="flex-value">
          <b>{{phase2ExpenseMinutesElapsed}} mins.</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Additional hours saved:</div>
        <div class="flex-value">
          <b>{{phase2ExpenseHoursElapsed }} hrs.</b>
        </div>
      </div>
      <hr class="summary-hr" />

      <div class="flex-details-container">
        <div class="flex-label">Total minutes saved:</div>
        <div class="flex-value">
          <b>{{expenseMinutesElapsed + phase2ExpenseMinutesElapsed}} mins.</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">Total hours saved:</div>
        <div class="flex-value">
          <b>{{totalHoursSaved}} hrs.</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">
          Total business
          <b>work days saved</b>:
        </div>
        <div class="flex-value">
          <b style="color:red;">{{totalBizDaysSaved}} days</b>
        </div>
      </div>
      <div class="flex-details-container">
        <div class="flex-label">
          <b>Total DAYS I regained of my life!</b>
        </div>
        <div class="flex-value">
          <b style="color:red;">{{totalDaysSaved}} days!</b>
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
      phase2StartDate: new Date(2021, 11, 1),
      phase2ExpenseTaskMinutes: 5,
      phase2ExpenseMinutesElapsed: 0,
      phase2ExpenseHoursElapsed: 0,
      phase2ExpenseMonthsElapsed: 0,
      phase2ExpenseBizDaysSaved: 0,
      phase2ExpenseDaysSaved: 0,
      totalHoursSaved: 0,
      totalBizDaysSaved: 0,
      totalDaysSaved: 0,
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
    getPhase2StartDate: function () {
      return (
        this.phase2StartDate.getMonth() +
        1 +
        "/" +
        this.phase2StartDate.getDate() +
        "/" +
        this.phase2StartDate.getFullYear()
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
      // Get the number of months that have elapsed
      var monthDifference = differenceInMonths(this.startDate, this.todaysDate);

      this.expenseMonthsElapsed = monthDifference;

      // Set the data elements based on the calculated and filtered days
      this.expenseMinutesElapsed =
        this.expenseMonthsElapsed * this.expenseTaskMinutes;
      this.expenseHoursElapsed = (this.expenseMinutesElapsed / 60).toFixed(2);
      this.expenseBizDaysSaved = (this.expenseHoursElapsed / 8).toFixed(2);
      this.expenseDaysSaved = (this.expenseHoursElapsed / 24).toFixed(2);

      // Phase 2 Calcs

      // Get the number of months that have elapsed in phase 2
      var phase2MonthDifference = differenceInMonths(
        this.phase2StartDate,
        this.todaysDate
      );

      // Add one iteration to the months elapsed to reflect the expense report running
      // the same month it was implemented - so the months would've been zero even
      // though the benefit was realized
      this.phase2ExpenseMonthsElapsed = phase2MonthDifference + 1;

      this.phase2ExpenseMinutesElapsed =
        this.phase2ExpenseMonthsElapsed * this.phase2ExpenseTaskMinutes;
      this.phase2ExpenseHoursElapsed = (
        this.phase2ExpenseMinutesElapsed / 60
      ).toFixed(2);
      this.phase2ExpenseBizDaysSaved = (
        this.phase2ExpenseHoursElapsed / 8
      ).toFixed(2);
      this.phase2ExpenseDaysSaved = (
        this.phase2ExpenseHoursElapsed / 24
      ).toFixed(2);

      this.totalHoursSaved = (
        parseFloat(this.expenseHoursElapsed) +
        parseFloat(this.phase2ExpenseHoursElapsed)
      ).toFixed(2);

      this.totalBizDaysSaved = (
        parseFloat(this.expenseBizDaysSaved) +
        parseFloat(this.phase2ExpenseBizDaysSaved)
      ).toFixed(2);
      this.totalDaysSaved = (
        parseFloat(this.expenseDaysSaved) +
        parseFloat(this.phase2ExpenseDaysSaved)
      ).toFixed(2);

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
