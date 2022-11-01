<template>
  <div class="charts">
    <h1 class="animated bounceInRight">Bitcoin Price Index History</h1>

    <div class="loading animated bounceInRight" v-if="loading">
      <p>Loading...</p>
    </div>

    <div class="error animated bounceInRight" v-else-if="showError">
      <p class="big">🙁</p>
      <p>Error accessing the API: {{ error.message }}</p>
      <p v-if="error.response">Response: {{ error.response }}</p>
    </div>

    <div class="animated bounceInRight" v-else>

      <!-- Vue Component -->
      <LineChartJs :data="chartData" :options="chartOptions"/>

      <p class="updated">Updated: {{ updated }}</p>
      <p class="box disclaimer">{{ disclaimer }}</p>
    </div>
  </div>
</template>

<script>
  import LineChartJs from '../components/LineChartJs.vue';
  import axios from 'axios';
  import * as moment from "moment";

  export default {
    name: 'ChartJsLineChart',
    components: {
      LineChartJs,
    },
    methods: {
        async getData() {

        try {
          // Get data method uses axios to get data via a HTTP API Endpoint
          const response = await axios.get('https://api.coinstats.app/public/v1/charts?period=1m&coinId=bitcoin');
          this.chartData.labels = response.data.chart.map((value) =>  moment(value[0] * 1000).format('YYYY-MM-DD'))
          this.chartData.datasets[0].data = response.data.chart.map((value) => value[1])
          // Assign the last updated time
          this.updated = moment().format('YYYY-MM-DD HH:mm:ss');

          // Assign the disclaimer text
          this.disclaimer = 'Data from coin stats api';
        } catch (error) {
          // Executes if an error occurs if code is not >= 200 && < 300
          this.showError = true;
          this.error = error;
        } finally {
          this.loading = false
        }
      },
    },

    /**
     * The data object for the Vue instance.
     * Must declare all root-level reactive properties upfront to be reactive.
     */
    data() {
      return {
        loading: true,
        updated: null,
        showError: false,
        error: null,
        chartData: {
          datasets: [
            {
              label: 'Bitcoin (BTC/USD)',
              backgroundColor: '#f7931a',
              borderColor: '#f7931a',
              fill: false,
              data: null,
            },
          ],
        },
        chartOptions: {
          responsive: true,
          maintainAspectRatio: false,
          tooltips: {
            enabled: true,
          },
          scales: {
            yAxes: [
              {
                ticks: {
                  callback: (value) => '$' + value,
                },
              },
            ],
          },
        },
      };
    },

    /**
     * Called after the instance has been mounted
     */
    mounted() {
      this.getData();
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
