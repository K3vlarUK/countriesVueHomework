<template lang="html">
  <div>
    <h1>Countries App</h1>
    <div class="page-container">
      <div class="country-list">
        <country-select :countries="countries"></country-select>
      </div>
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
h1 {
  text-align: center;
}

.page-container {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.country-list {
  flex: 50%;
  align-content: center;
}

.country-info {
  flex: 50%;
  align-content: center;
}
</style>
