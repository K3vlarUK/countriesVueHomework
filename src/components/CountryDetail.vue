<template lang="html">
  <div v-if="country">
    <img :src="country.flag" alt="flag of the country">
    <h3>{{ country.name }}</h3>
    <p>Population: {{ country.population }}</p>
    <p>Capital City: {{ country.capital }}</p>
    <p>Spoken Languages</p>
    <ul>
      <li v-for="language in country.languages">
        {{ language.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'country-detail',
  props: ['country']
}
</script>

<style lang="css" scoped>
img {
  width: 200px;
  height: auto;
}
</style>
