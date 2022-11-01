<template>
  <div id="overview">

    <h1 class="animated bounceInLeft">Top 10 Cryptos</h1>

    <div class="box loading" v-if="loading">
      <p>Loading...</p>
    </div>

    <div class="box error" v-else-if="showError">
      <p class="big">🙁</p>
      <p>Error accessing the API: {{ error.message }}</p>
      <p v-if="error.response">Response: {{ error.response }}</p>
    </div>

    <div class="box animated bounceInLeft" v-else>

      <div v-for="currency in currencies" :key="currency.symbol">

        <span>{{ currency.name }} ({{ currency.symbol }}):</span>

        <span class="highlight right">
          <span>USD</span> {{ currency['price'] | currencyDecimal }}
        </span>
      </div>
    </div>

    <div class="updated animated bounceInLeft" v-if="!showError">Updated: {{ updated }}</div>

  </div>
</template>

<script>
  import axios from 'axios';
  import * as moment from 'moment/moment'

  export default {
    name: 'Overview',
    data() {
      return {
        currencies: null,
        updated: null,
        loading: true,
        showError: false,
        error: null,
      };
    },
    async mounted() {
      try {
        //Get data method uses axios to get data via a HTTP API Endpoint
        const response = await axios.get('https://api.coinstats.app/public/v1/coins?skip=0&limit=10&currency=USD');
        this.currencies = response.data['coins'];
        this.updated = moment().format('YYYY-MM-DD HH:mm:ss');
      } catch(error) {
        // Executes if an error occurs if code is not >= 200 && < 300
        this.showError = true;
        this.error = error;
      }finally {
        this.loading = false
      }
    },
    filters: {
      currencyDecimal(value) {
        return value.toFixed(2);
      },
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
