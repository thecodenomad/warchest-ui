<template>
  <div>
    <h1>Warchest!</h1>
    <div v-if="wc_coins.length == 0">Sad day, no coins!</div>
    <div v-else>
      <div v-for="(coin, symbol) in wc_coins" :key="symbol" class="wc-card -shadow">
      <h4 class="title">{{ symbol }}</h4>
      <div class="wc-card-num-coins">
        <p><font-awesome-icon class="wc-coins" icon="coins" />{{ coin.amount }}</p>
      </div>
      <div class="wc-card-stats">
        <p v-if="coin.amount*coin.rates.USD > 0">
          <span class="profitable">${{ coin.amount*coin.rates["USD"]}}</span>
        </p>
        <p v-else>
          <span class="red-alert">${{ coin.amount*coin.coin_rates["USD"]}}</span>
        </p>
        <p> Transaction(s): {{ coin.transactions.length }} </p>
      </div>
    </div>
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
