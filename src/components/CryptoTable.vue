<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Crypto Prices</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-content>
        <div class="container">
          <ion-button @click="fetchData" color="primary">Get Data</ion-button>
          
          <div class="table-container" v-if="cryptoData.length > 0">
            <table>
              <thead>
                <tr>
                  <th>Name</th>
                  <th>Symbol</th>
                  <th>Harga USD</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(crypto, index) in cryptoData" :key="index">
                  <td>{{ crypto.name }}</td>
                  <td>{{ crypto.symbol }}</td>
                  <td>{{ crypto.price_usd }}</td>
                </tr>
              </tbody>
            </table>
          </div>
  
          <div v-else>
            <p>No data available. Click "Get Data" to fetch cryptocurrency prices.</p>
          </div>
        </div>
      </ion-content>
    </ion-page>
  </template>
  
  <script>
  import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonButton } from '@ionic/vue';
  import axios from 'axios';
  
  export default {
    name: 'CryptoTable',
    components: {
      IonPage,
      IonHeader,
      IonToolbar,
      IonTitle,
      IonContent,
      IonButton,
    },
    data() {
      return {
        cryptoData: [],  // Array untuk menyimpan data kripto
      };
    },
    methods: {
      async fetchData() {
        try {
          const response = await axios.get('https://api.coinlore.net/api/tickers/');
          this.cryptoData = response.data.data.map((crypto) => ({
            name: crypto.name,
            symbol: crypto.symbol,
            price_usd: crypto.price_usd,
          }));
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .container {
    padding: 16px;
    text-align: center;
  }
  
  .table-container {
    overflow-x: auto;
    margin-top: 16px;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
    text-align: left;
  }
  
  th, td {
    padding: 8px;
    border: 1px solid #ddd;
  }
  
  th {
    background-color: #f2f2f2;
  }
  
  ion-button {
    margin-bottom: 16px;
  }
  </style>
  