<template>
<v-app>
    <v-main>
      <div class="container">
        <div class="row">
          <div class="col">
            <v-card class="elevation-1" dark>
                  <v-card-title>
                      <h2>Crypto Prices</h2>
                    <v-spacer></v-spacer>
                          <v-text-field v-model="search" label="Search for your currency..." single-line hide-details></v-text-field>
                    <v-card-text>
                        <v-data-table :headers="headers" :search="search" :items="currencies" :items-per-page="100" :hide-default-footer="true" disable-pagination></v-data-table>
                    </v-card-text>
                  </v-card-title>
              </v-card>
          </div>
        </div>
      </div>     
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  data () {
    return{
      currencies: [],
      headers: [
        {text:'Name', value: 'CoinInfo.FullName', sortable: false,}, 
        {text:'Ticker', value:'CoinInfo.Name', sortable: false,}, 
        {text:'Price', value:'DISPLAY.GBP.PRICE', sortable: false,}, 
        {text:'1H%', value:'DISPLAY.GBP.CHANGEPCTHOUR', sortable: false,}, 
        {text:'24H%', value:'DISPLAY.GBP.CHANGEPCT24HOUR', sortable: false,}, 
        {text:'Day\'s Low', value:'DISPLAY.GBP.LOWDAY', sortable: false,}, 
        {text:'Day\'s High', value:'DISPLAY.GBP.HIGHDAY', sortable: false,}, 
        {text:'Market Cap', value:'DISPLAY.GBP.MKTCAP', sortable: false,}
        ],
      search:'',
    } 
  }, 

  mounted () {
    this.$axios.get('https://min-api.cryptocompare.com/data/top/mktcapfull?limit=100&tsym=GBP&api_key=ADDYOURAPIKEYHERE!')
      .then((result) => {
        this.currencies = result.data;
        this.currencies = this.currencies.Data;
        console.log(this.currencies);
      })
  },

};

</script>