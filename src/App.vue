<template>
  <div id="app">
    <WarchestWallet/>
  </div>
</template>

<script>
import WarchestWallet from './components/WarchestWallet.vue'

export default {
  name: 'App',
  components: {
    WarchestWallet
  }
}
</script>

<!--
Styles Taken from:
Reference: https://www.vuemastery.com/courses/real-world-vue-js/single-file-vue-components
Lesson 6 - https://github.com/Code-Pop/real-world-vue
-->
<style>
html {
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
body {
  margin: 0;
  font-family: 'Open Sans', sans-serif;
  font-size: 16px;
  line-height: 1.5;
}
#app {
  box-sizing: border-box;
  width: 500px;
  padding: 0 20px 20px;
  margin: 0 auto;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  display: flex;
  align-items: center;
  font-family: 'Montserrat', sans-serif;
}
h1 {
  font-size: 50px;
  font-weight: 700;
}
h2 {
  font-size: 38px;
  font-weight: 700;
}
h3 {
  font-size: 28px;
  font-weight: 700;
}
h4 {
  font-size: 21px;
  font-weight: 700;
}
h5 {
  font-size: 16px;
  font-weight: 700;
}
h6 {
  font-size: 15px;
  font-weight: 700;
}
</style>
