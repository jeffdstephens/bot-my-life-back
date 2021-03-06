<template >
  <div class="CovidBotCounter">
    <h2>Daily COVID-19 Team Status Report Bot</h2>
    <div>
      <h4>
        This automation collects the developers' daily statuses from Slack and emails a single nightly status report for the team. To learn more about the details, check out
        <a
          href="https://www.jeffdstephens.com/posts/status-report-automation/"
          target="_blank"
        >the blog post</a> where I show you how it's done. This automation runs every night, Monday-Friday. The time it took to complete this task manually was 30 mins. while the automation process is fully automated, resulting in personal time savings of 30 mins. per day.
      </h4>
      <p>
        Start date (the day my bot started doing the team status for me):
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
        <b>{{statusTaskMinutes}} mins.</b>
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
  </div>
</template>

<script>
import differenceInBusinessDays from "date-fns/differenceInBusinessDays";
import { inRange } from "@18f/us-federal-holidays";

export default {
  name: "CovidBotCounter",
  props: {},
  data: function () {
    return {
      startDate: new Date(2020, 4, 19),
      todaysDate: new Date(),
      statusTaskMinutes: 30,
      statsuDaysElapsed: 0,
      statusMinutesElapsed: 0,
      statusHoursElapsed: 0,
      statusBizDaysSaved: 0,
      statusDaysSaved: 0,
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
