<template>
  <div id="chart" class="deaths-container">
    <h3>Death cases</h3>
    <apexchart
      type="area"
      height="350"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
import Vue from "vue";
import VueApexCharts from "vue-apexcharts";
Vue.use(VueApexCharts);

Vue.component("apexchart", VueApexCharts);
export default {
  name: "DeathsChart",
  props: {
    all_data: {},
  },
  data: () => {
    return {
      chartOptions: {
        dataLabels: {
          enabled: false,
        },
        colors: ["#8b0000"],
        chart: {
          id: "vuechart-example",
        },
        xaxis: {
          categories: [],
        },
      },
      series: [
        {
          name: "Deaths",
          data: [],
        },
      ],
    };
  },
  created() {
    let deaths = [];
    let dates = [];

    this.all_data.map((item, key) => {
      deaths.push(item.deaths);
      dates.push(item.date);
    });

    this.series = [
      {
        name: "deaths",
        data: deaths,
      },
    ];
    this.chartOptions = {
      colors: ["#8b0000"],
      dataLabels: {
        enabled: false,
      },
      xaxis: {
        type: "datetime",
        categories: dates,
      },
      tooltip: {
        x: {
          format: "dd/MMM/yyyy",
        },
      },
    };
  },
};
</script>

<style scoped>
.deaths-container {
  margin: 50px auto;
}
h3 {
  font-size: 22px;
  font-weight: 400;
}
</style>