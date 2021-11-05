<template>
  <div class="wc-wallet">
    <h2>Warchest!</h2>
    <v-divider></v-divider>
    <div v-if="errored || wc_coins.length == 0">
      <img src="@/assets/sad-panda.png">
      <h3 class="sad-panda-text">Sad day. No coins!</h3>
    </div>
    <div v-else>
      <v-card v-for="(coin, symbol) in wc_coins" :key="symbol" class="mx-auto wc-card" outlined>
        <v-img
            src=""
            class="white--text align-end"
            gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
            height="200px"
        >
          <v-card-title v-text="symbol"></v-card-title>
          <v-card-subtitle>${{ coin.amount*coin.rates["USD"]}}</v-card-subtitle>
        </v-img>

        <v-card-text>
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
        </v-card-text>
      </v-card>
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
.sad-panda-text {
  text-align: center;
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

.wc-button {
  margin: 5px;
}

.sad-panda {
  margin-top: 20px;
  margin-bottom: 20px;
}

.wc-link {
  color: black;
  text-decoration: none;
  font-weight: 100;
}
.red-alert {
  color: darkred;
}
.profitable {
  color: darkgreen;
  text-blink: 1s;
  font-weight: bolder;
}
.wc-coins {
  padding-right: 10px;
}
.wc-card-stats {
  text-align: left;
}
</style>
