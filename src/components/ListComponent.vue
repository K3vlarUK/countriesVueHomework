<template lang="html">
  <li @click="clickHandler">{{ country.name }}</li>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name:'list-component',
  props: ['country'],
  methods: {
    clickHandler(){
      eventBus.$emit('country-selected', this.country)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
