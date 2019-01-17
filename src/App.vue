<template>
<div id="app">
  <h1>Will the Tax Hike Affect Me?</h1>
  <p>In a <a href="https://www.cnn.com/2019/01/04/politics/alexandria-ocasio-cortez-tax-climate-change-plan/index.html">60 Minutes interview</a>, Alexandria Ocasio-Cortez (D-NY) proposed a <b>70%</b> marginal income tax rate for Americans earning <b>$10,000,000</b> or more.</p>
  <p>This calculator will help you figure out how such a tax will affect you.</p>
  <h2>How much did you make last year?</h2>
  <vue-numeric id="income" currency="$" separator="," :empty-value="24000" v-model="income"></vue-numeric>
  <div id="results">
    <h2>Are you affected?</h2>
    <p>{{ results }}</p>
  </div>
  <a href="https://www.irs.gov/pub/irs-soi/soi-a-ints-id1801.pdf">source</a>
</div>
</template>

<script>
import VueNumeric from 'vue-numeric'

export default {
  name: 'app',
  components: {
    VueNumeric
  },
  data () {
    return {
      income: ''
    }
  },
  computed: {
    results() {
      if (this.income < 79655) {
        return "No."
      } else if (this.income >= 79655 && this.income < 138031) {
        return "No, but congrats on being in the top 25%!"
      } else if (this.income >= 138031 && this.income < 195778) {
        return "No, but congrats on being in the top 10%!"
      } else if (this.income >= 195778 && this.income <  480930) {
        return "No, but congrats on being in the top 5%!"
      } else if (this.income >= 480930 && this.income < 2220264) {
        return "No, but congrats on being in the top 1%!"
      } else if (this.income >= 2220264 && this.income <= 10000000) {
        return "No, but congrats on being in the top 0.1%!"
      } else {
        return "Yes. We're sorry for your loss."
      }
    }
  }
}
</script>

<style>
p {



}
#app {
  font-family: Grande, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0 auto;
  padding: 1em;
  max-width: 50em;
  text-align: justify;
  
}
#income {
  font-size: 1.5em;
}
</style>
