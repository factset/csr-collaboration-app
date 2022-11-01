<template>
  <div class="charts">
    <h1 class="animated bounceInRight">Bitcoin Price Index History</h1>

    <div class="loading animated bounceInRight" v-if="loading">
      <p>Loading...</p>
    </div>

    <div class="error animated bounceInRight" v-else-if="showError">
      <p>Error accessing the API: {{ error.message }}</p>
      <p v-if="error.response">Response: {{ error.response }}</p>
    </div>

    <div class="animated bounceInRight" v-else>
      <highcharts :constructor-type="'stockChart'" :options="chartOptions"></highcharts>
      <p class="updated">Updated: {{ updated }}</p>
      <p class="box disclaimer">{{ disclaimer }}</p>
    </div>
  </div>
</template>

<script>
  import * as moment from 'moment';
  import axios from 'axios';

  export default {
    name: 'HighChartLineChart',
    methods: {

      async getData() {
        try {
          // Get data method uses axios to get data via a HTTP API Endpoint
          const response = await axios.get('https://api.coinstats.app/public/v1/charts?period=1m&coinId=bitcoin');

          // Parse the response data into a format that highcharts understands
          this.chartOptions.series[0].data = this.parseData(response.data.chart);

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
      /**
       * Parse data function
       */
      parseData(data) {
        return data.map((value) => [value[0] * 1000, value[1]])
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
        chartOptions: {
          title: {
            text: '',
          },
          series: [
            {
              name: 'Bitcoin (BTC/USD)',
              type: 'spline',
              color: '#f7931a',
              data: null,
              marker: {
                enabled: true,
                radius: 4
              }
            },
          ],
          navigator: {
            enabled: false,
          },
          scrollbar: {
            enabled: false,
          },
          rangeSelector: {
            enabled: false,
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
