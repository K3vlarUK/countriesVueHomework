<template lang="html">
  <div>
    <select @change="selectHandler" v-model="country">
      <option v-for="country in countries" :value="country">{{ country.name }}</option>
    </select>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'country-select',
  data(){
    return{
      country: null
    }
  },
  props: ['countries'],
  methods: {
    selectHandler(){
      eventBus.$emit('country-selected', this.country)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
