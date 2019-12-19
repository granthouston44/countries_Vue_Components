<template lang="html">
  <div>
    <!-- <ul>
    <countryListItem v-for="(country, index) in allCountries" :country="country" :key="index">{{country.name}}</countryListItem>
  </ul> -->
  <select @change="handleChange" v-model="selectedCountry">
    <option disabled value="">Select a Country</option>
    <option v-for="(country, index) in allCountries" :value="country" :key="index">{{country.name}}</option>
  </select>
</div>

</template>

<script>
import CountryComponent from './CountryComponent.vue'
import {eventBus} from '../main.js';

export default {
  name: 'country-list',
  data(){
    return {
      selectedCountry: null
    }
  },
  props: ['allCountries'],
  components: {
    "countryListItem": CountryComponent
  },
  methods: {
    handleChange(event){
      //this emits the data from this vue file (selectedCountry)
      //but where we listen for this data we can assign it to any varibale name we want
      //such as selected banana
      eventBus.$emit('country-selected', this.selectedCountry)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
