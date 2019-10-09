<template lang="html">
  <div>
    <h1>Countries App</h1>
    <div class="page-container">
      <div class="country-list">
        <countries-list :countries="countries"></countries-list>
      </div>
      <div class="country-info">
        <country-detail :country="selectedCountry"></country-detail>
      </div>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js';
import CountriesList from './components/CountriesList.vue';
import CountryDetail from './components/CountryDetail.vue';

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
    "countries-list": CountriesList,
    "country-detail": CountryDetail
  }
}
</script>

<style lang="css" scoped>
.page-container {
  display: flex;
  flex-flow: wrap;
}

.country-list {
  flex: 50%;
  justify-content: center;
}

.country-detail {
  flex: 50%;
  justify-content: center;
}
</style>
