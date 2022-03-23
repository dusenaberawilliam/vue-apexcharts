<template>
  <div id="chart" class="chart">
    <h3>Confirmed and Recovered cases</h3>
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
  name: "Chart",
  props: {
    all_data: {},
  },
  data: () => {
    return {
      chartOptions: {
        dataLabels: {
          enabled: false,
        },
        colors: ["#6495ed", "#66DA26"],
        chart: {
          id: "vuechart-example",
        },
        xaxis: {
          categories: [],
        },
      },
      series: [
        {
          name: "Confirmed",
          data: [],
        },
        {
          name: "Recovered",
          data: [],
        },
      ],
    };
  },
  created() {
    let confirmed = [];
    let recovered = [];
    let dates = [];
    this.all_data.map((item, key) => {
      confirmed.push(item.confirmed);
      recovered.push(item.recovered);
      dates.push(item.date);
    });
    // this.all_data.map((item, key) => {
    //   deaths.push(item.deaths);
    //   dates.push(item.date);
    // });

    this.series = [
      {
        name: "Confirmed",
        data: confirmed,
      },
      {
        name: "Recovered",
        type: "column",
        data: recovered,
      },
    ];
    this.chartOptions = {
      xaxis: {
        type: "datetime",
        categories: dates,
      },
      dataLabels: {
        enabled: false,
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
h3 {
  font-size: 22px;
  font-weight: 400;
}
</style>