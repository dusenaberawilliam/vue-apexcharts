<template>
  <div id="app" class="charts-container">
    <h2>Covid19 Smartable</h2>
    <div class="card">
      <!-- <div>
        <h4>Active cases</h4>
        <p>2000</p>
      </div> -->
      <div>
        <h4>Confirmed cases</h4>
        <p>{{ totalConfirmedCases }}</p>
      </div>
      <div>
        <h4>Recovered</h4>
        <p>{{ totalRecoveredCases }}</p>
      </div>
      <div>
        <h4>Deaths</h4>
        <p>{{ totalDeaths }}</p>
      </div>
    </div>
    <chart v-if="all_data" :all_data="all_data" />
    <deaths-chart v-if="all_data" :all_data="all_data" />
    <pie-chart v-if="allStats" :allStats="allStats" />
  </div>
</template>

<script>
import Chart from "./components/Chart.vue";
import DeathsChart from "./components/DeathsChart.vue";
import PieChart from "./components/PieChart.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Chart,
    DeathsChart,
    PieChart,
  },
  data() {
    return {
      all_data: null,
      allStats: null,
      totalConfirmedCases: 0,
      totalRecoveredCases: 0,
      totalDeaths: 0,
    };
  },
  mounted() {
    axios
      .get("https://coronavirus-smartable.p.rapidapi.com/stats/v1/RW/", {
        headers: {
          "x-rapidapi-host": "",
          "x-rapidapi-key": "",
        },
      })
      .then((response) => {
        // console.log(response.data.stats.history);
        this.totalConfirmedCases = response.data.stats.totalConfirmedCases;
        this.totalRecoveredCases = response.data.stats.totalRecoveredCases;
        this.totalDeaths = response.data.stats.totalDeaths;
        this.allStats = response.data.stats;
        this.all_data = response.data.stats.history;
      });
  },
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
}
#app {
  font-family: System-ui;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
.charts-container {
  width: 98%;
}
.charts-container h2 {
  font-size: 40px;
}
.card {
  width: 60%;
  margin: 20px auto;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.card div {
  width: 220px;
  border: 1px solid #2c3e50;
  margin: 5px 0;
}
h4 {
  font-weight: 400;
  font-size: 20px;
  margin: 2px;
}
p {
  font-weight: 500;
  font-size: 30px;
  margin: 2px;
}
</style>
