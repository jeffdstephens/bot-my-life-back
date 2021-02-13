<template >
  <div class="BotCounter">
    <p>This website shows how I got my life back by implementing bots and automation. These bots help me take care of some of the menial tasks throughout the day so I can do more of the things that I truly love.</p>
  </div>
  <h2>COVID-19 Daily Status Report Bot</h2>
  <div>
    <h4>
      This automation collects the developers' daily statuses from Slack and emails a single nightly status report for the team. To learn more about the details, check out
      <a
        href="https://www.jeffdstephens.com/posts/status-report-automation/"
        target="_blank"
      >the blog post</a> where I show you how it's done.
    </h4>
    <p>
      Start date (the day my bot started doing my status for me):
      <b>{{ getStartDate }}</b>
    </p>
    <p>
      Today's date:
      <b>{{ getTodaysDate }}</b>
    </p>
    <p>
      Total number of business days elapsed (excluding weekends and U.S. federal holidays):
      <b>{{ getDayDifferenceAndCalcs() }}</b>
    </p>
    <p>
      Time to complete task (per night):
      <b>{{statusTaskMinutes}}</b>
    </p>
    <p>
      Total minutes saved:
      <b>{{statusMinutesElapsed}}</b>
    </p>
    <p>
      Total hours saved:
      <b>{{statusHoursElapsed }}</b>
    </p>
    <p>
      Total business
      <b>work days saved</b>:
      <b>{{statusBizDaysSaved }}</b>
    </p>
    <h3>
      Total DAYS I regained of my life!
      {{statusDaysSaved}}
    </h3>
  </div>
</template>

<script>
import differenceInBusinessDays from "date-fns/differenceInBusinessDays";
import { inRange } from "@18f/us-federal-holidays";

export default {
  name: "BotCounter",
  props: {},
  data: function () {
    return {
      startDate: new Date("5-19-2020"),
      todaysDate: new Date(),
      statusTaskMinutes: 30,
      statsuDaysElapsed: 0,
      statusMinutesElapsed: 0,
      statusHoursElapsed: 0,
      statusBizDaysSaved: 0,
      statusDaysSaved: 0,
      expenseTaskMinutes: 20,
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
    getOPMHolidays: function () {
      const options = {
        shiftSaturdayHolidays: true,
        shiftSundayHolidays: true,
      };
      // Find the holidays in the given date range
      const holidays = inRange(this.startDate, this.todaysDate, options);

      // Return the number of holidays that occured
      return holidays.length;
    },
    getDayDifferenceAndCalcs: function () {
      // Get the number of business days - week days - that have elapsed
      var bizDayDifference = differenceInBusinessDays(
        this.todaysDate,
        this.startDate
      );

      // Subtract the number of OPM stipulated federal holidays during that time
      this.statsuDaysElapsed = bizDayDifference - this.getOPMHolidays();

      // Set the data elements based on the calculated and filtered days
      this.statusMinutesElapsed =
        this.statsuDaysElapsed * this.statusTaskMinutes;
      this.statusHoursElapsed = (this.statusMinutesElapsed / 60).toFixed(2);
      this.statusBizDaysSaved = (this.statusHoursElapsed / 8).toFixed(2);
      this.statusDaysSaved = (this.statusHoursElapsed / 24).toFixed(2);

      return this.statsuDaysElapsed;
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
h2 {
  color: #42b983;
}
a {
  color: #42b983;
}
</style>
