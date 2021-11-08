<template>
  <div class="wc-wallet">
    <h2>Warchest!</h2>
    <v-divider></v-divider>
    <div v-if="!errored && Object.keys(wc_coins).length === 0">
      <img class="sad-panda-img" src="@/assets/sad-panda.png" alt="">
      <h3 class="sad-panda-text">Sad day. No coins found.</h3>
    </div>
    <div v-else-if="errored">
      <img src="@/assets/sad-panda.png" alt="">
      <h3 class="sad-panda-text">Sad day. Config issue. U haz API kayz?</h3>
    </div>
    <div v-else>
      <v-container>
        <v-row>
          <v-col cols="12">
            <v-card v-for="(coin, symbol) in wc_coins" :key="symbol" class="wc-card mx-auto">
              <v-card-text>
                <v-row align="center"><v-col><h2>{{ symbol }}</h2></v-col></v-row>
                <v-row align="center">
                  <v-col
                    class="text-h2"
                    cols="8"
                  >
                    <v-row>
                      <v-col>
                        <v-chip v-if="coin.profit > 0" class="ma-2 profitable wc-stats">
                          <v-icon large left>mdi-arrow-top-right</v-icon> {{ formatCurrency(coin.profit) }}
                        </v-chip>
                        <v-chip v-else class="ma-2 red wc-stats">
                          <v-icon large>mdi-arrow-bottom-right</v-icon>{{ formatCurrency(coin.profit) }}
                        </v-chip>
                      </v-col>
                    </v-row>
                    <v-row>
                      <v-col>
                        <v-chip class="ma-2 wc-cost">
                          <v-icon large>mdi-currency-usd</v-icon>Investment: {{ formatCurrency(coin.profit) }}
                        </v-chip>
                      </v-col>
                    </v-row>

                  </v-col>
                  <v-col cols="4">
                    <v-img class="wc-coin-img" :src="coin.image_uri" width="125px"></v-img>
                  </v-col>
                </v-row>
              </v-card-text>
              <v-card-actions>
                <v-btn class="wc-button">
                  <v-icon>mdi-fire</v-icon>
                </v-btn>
                <v-btn class="wc-button">
                  <v-icon>mdi-chart-line</v-icon>
                  Stats
                </v-btn>
                <v-btn class="wc-button">
                  <v-icon>mdi-format-list-bulleted</v-icon>
                  Transactions
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data(){
    return {
      name: "WarchestWallet",
      wc_coins: [],
      loading: false,
      errored: false
    }
  },
  async created () {
    try {
      console.log("Querying backend for coins...")
      const response = await axios.get('http://localhost:8080/api/wallet')
      this.wc_coins = response.data.coins
    } catch (e) {
      this.errored = true
      console.log("Failed! This is why: "+e)
      this.wc_coins = {}
    }
  },
  methods:{
    formatCurrency: function (currency) {
      currency = currency.toFixed(2);
      return currency
    }
  }
}
</script>

<!--
Styles Taken from:
Reference: https://www.vuemastery.com/courses/real-world-vue-js/single-file-vue-components
Lesson 6 - https://github.com/Code-Pop/real-world-vue
-->
<style scoped>
h3 {
  padding-top: 25px;
  padding-bottom: 25px;
}
.wc-card {
  padding: 20px;
  margin-bottom: 5px;
  transition: all 0.2s linear;
  cursor: pointer;
}
.wc-card:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2), 0 1px 15px 0 rgba(0, 0, 0, 0.19);
}
.wc-card > .title {
  margin: 0;
}

.wc-coin-img {

}

.wc-button {
  margin: 5px;
}

.sad-panda-img {
  margin-top: 20px;
  margin-bottom: 20px;
}

.wc-coin-stats {
  padding-top: 15px;
  font-size: 20px;
}

.profitable i.v-icon.v-icon {
  color: green;
}

.red i.v-icon.v-icon {
  color: red;
}

.wc-cost i.v-icon.v-icon {
  color: darkcyan;
  font-size: 14px;
}

</style>
