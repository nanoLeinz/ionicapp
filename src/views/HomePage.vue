<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Harga Crypto</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <ion-button @click="fetchData">Get Data</ion-button>
      <ion-grid>
        <ion-row>
          <ion-col><strong>Name</strong></ion-col>
          <ion-col><strong>Symbol</strong></ion-col>
          <ion-col><strong>Price USD</strong></ion-col>
        </ion-row>
        <ion-row v-for="coin in coins" :key="coin.id">
          <ion-col>{{ coin.name }}</ion-col>
          <ion-col>{{ coin.symbol }}</ion-col>
          <ion-col>{{ coin.price_usd }}</ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Home',
  data() {
    return {
      coins: []
    };
  },
  methods: {
    fetchData() {
      axios.get('https://api.coinlore.net/api/tickers/')
        .then(response => {
          this.coins = response.data.data;
        })
        .catch(error => {
          console.error('Error fetching data:', error);
        });
    }
  }
};
</script>

<style scoped>
ion-grid {
  margin-top: 20px;
}
</style>