<template>
<div id="app">
  <h1>Will the Tax Hike Affect Me?</h1>
  <p>In a 60 Minutes interview, Alexandria Ocasio-Cortez (D-NY) proposed that in order to fund the Green New Deal, we institute a <b>70%</b> marginal income tax rate for Americans earning <b>$10,000,000</b> or more.</p>
  <p>This calculator will help you figure out how such a tax will affect you.</p>
  <h2>How much did you make last year?</h2>
  <vue-numeric id="income" currency="$" separator="," :empty-value="24000" v-model="income"></vue-numeric>
  <vue-slider ref="slider" max="11" interval=".01" tooltip="false" v-model="logIncome"></vue-slider>
  <div id="results">
    <h2>Are you affected?</h2>
    <p>{{ results }}</p>
  </div>
  <hr>
  <p><a href="https://www.cnn.com/2019/01/04/politics/alexandria-ocasio-cortez-tax-climate-change-plan/index.html">[1]</a>&nbsp;<a href="https://www.irs.gov/pub/irs-soi/soi-a-ints-id1801.pdf">[2]</a>&nbsp;<a href="https://www.businessinsider.com/what-amazon-ceo-jeff-bezos-makes-every-day-hour-minute-2018-10">[3]</a></p>
  <p><a href="https://github.com/mveytsman/willthetaxhikeaffect.me">Made</a> with 🤑 by <a href="https://twitter.com/mveytsman">mveytsman</a></p>
</div>
</template>

<script>
import VueNumeric from 'vue-numeric'
import vueSlider from 'vue-slider-component'


export default {
  name: 'app',
  components: {
    VueNumeric,
    vueSlider
  },
  data () {
    return {
      income: ''
    }
  },
  computed: {
    logIncome: {
      get() {
        if (this.income > 1) {
          return Math.log10(this.income)
        }
        else {
          return 0
        }
      },
      set(value) {
        this.income = 10**value;
      }
    },
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
      } else if (this.income > 10000000 && this.income < 78500000000) {
        return "Yes. We're sorry for your loss."
      } else {
        return "Yes. We're sorry to hear about the divorce Jeff."
      }
    }
  }
}
</script>

<style>
a {
    color: #2A5DB0;
    text-decoration: none;
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
