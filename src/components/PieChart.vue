<template>
  <div id="chart">
    <apexchart
      type="pie"
      width="700"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
</template>

<script>
export default {
  name: "PieChart",
  props: {
    allStats: {},
  },
  data: () => {
    return {
      series: [44, 55, 13],
      chartOptions: {
        chart: {
          width: 700,
          type: "pie",
        },
        labels: [],
        responsive: [
          {
            breakpoint: 480,
            options: {
              chart: {
                width: 200,
              },
              legend: {
                position: "bottom",
              },
            },
          },
        ],
      },
    };
  },
  created() {
    this.chartOptions = {
      labels: [
        "Total confirmed cases",
        "Total recovered cases",
        "Total deaths",
      ],
    };

    this.series = [
      this.allStats.totalConfirmedCases,
      this.allStats.totalRecoveredCases,
      this.allStats.totalDeaths,
    ];
  },
};
</script>

<style>
</style>