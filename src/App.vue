<template>

  <div>
    <h1>Countries</h1>
    <div class="main-container">

      <country-list :countries = "countries"></country-list>
      <country-detail :country = "selectedCountry"></country-detail>

    </div>
  </div>

</template>

<script>
import CountryDetail from './components/CountryDetail.vue';
import CountryList from './components/CountryList.vue';
import { eventBus } from './main.js';

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null

    };
  },
  mounted() {
  fetch('https://restcountries.eu/rest/v2/all')
  .then(res => res.json())
  .then(countries => this.countries = countries)
  eventBus.$on('country-selected', (country) => {
    this.selectedCountry = country;
  })
},
  // eventBus.$on
  components: {
    "country-list": CountryList,
    "country-detail": CountryDetail
  }
}
</script>

<style>
.main-container {
  display: flex;
  justify-content: space-between;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
