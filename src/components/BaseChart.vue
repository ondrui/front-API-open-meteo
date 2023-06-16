<template>
  <div>
    <highcharts class="hc" :options="chartOptions" ref="chart"></highcharts>
  </div>
</template>

<script>
import Highcharts from "highcharts";
import exportingInit from "highcharts/modules/exporting";

exportingInit(Highcharts);

export default {
  data() {
    return {
      chartOptions: {
        series: [
          {
            data: [1, 2, 3]
          }
        ]
      }
    };
  },
  mounted() {
    this.loadData();
  },
  methods: {
    async loadData() {
      try {
        const res = await fetch('http://localhost:3002/api');
        const datasets = await res.json();
        this.chartOptions.series[0].data = datasets.data.map(({ temp }) => temp);
        console.log(datasets);
      } catch (error) {
        console.log('Error! Could not reach the server. ' + error);
      }
    }
  }
};
</script>

<style lang="scss" scoped></style>
