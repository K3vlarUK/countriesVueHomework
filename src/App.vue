<template lang="html">
  <div>
    <h1>Countries App</h1>
    <h3>Select a country to find out more</h3>
    <div class="page-container">
      <div class="country-list">
        <country-select :countries="countries"></country-select>
      </div>
      <br>
      <div class="country-info">
        <country-detail :country="selectedCountry"></country-detail>
      </div>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';
import CountryDetail from './components/CountryDetail.vue';
import CountrySelect from './components/CountrySelect.vue';

export default {
  name: 'app',
  data() {
    return {
      countries: [],
      selectedCountry: null
    };
  },
  mounted() {
    fetch('https://restcountries.eu/rest/v2/all')
    .then(result => result.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (country) => {
      this.selectedCountry = country;
    })
  },
  components: {
    "country-detail": CountryDetail,
    "country-select": CountrySelect
  }
}
</script>

<style lang="css" scoped>

.page-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

body {
  background-color: ghostWhite;
}

.country-info {
  background-color: aliceBlue;
  padding: 2rem;
  border: 2px solid black;
}

h1 {
  text-align: center;
  background-color: aliceBlue;
  color: navy;
  padding: 2rem;
  margin: -0.5rem;
  border-bottom: 2px solid black;
  font-style: helvetica;
}

h3 {
  text-align: center;
  font-style: helvetica;
}

</style>
