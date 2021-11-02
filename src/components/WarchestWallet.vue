<template>
  <div class="wc-card -shadow">
    <h4 class="title">{{ wc_coins[0].coin_symbol }}</h4>
    <p><font-awesome-icon class="wc-coins" icon="coins" />{{ wc_coins[0].amount }}</p>
    <p v-if="wc_coins[0].amount*wc_coins[0].coin_rates.USD > 0">
      Current Net Profit: <span class="profitable">${{ wc_coins[0].amount*wc_coins[0].coin_rates["USD"]}}</span>
    </p>
    <p v-else>
      Current Net Profit: <span class="red-alert">${{ wc_coins[0].amount*wc_coins[0].coin_rates["USD"]}}</span>
    </p>
    <p> Transaction(s): {{ wc_coins[0].transactions.length }} </p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      name: "WarchestWallet",
      wc_coins: [
        {
          account_id: "some-thing-long",
          cost: "0.27",
          amount: "1.0",
          coin_rates: {
            "EUR": "0.23",
            "GBP": "0.19",
            "USD": "0.28"
          },
          coin_symbol: 'DOGE',
          transactions: [
            {
              "num_coins": "1.0",
              "purchased_price": "0.2700",
              "transaction_fee": ".001"
            }
          ]
        }
      ]
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
  margin-bottom: 24px;
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
</style>
