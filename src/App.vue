<template>
<div>
  <h1>countries</h1>
  <div class="main-container">
      <country-list :allCountries="countries"/>
      <country-detail :country="selectedCountry"/>
  </div>
</div>
</template>

<script>
import CountriesList from './components/CountryList.vue';
import {eventBus} from './main.js'
import CountryDetail from './components/CountryDetails.vue';

export default {
  data(){
    return {
      countries: [],
      selectedCountry: null
    };

  },
  mounted(){
    fetch("https://restcountries.eu/rest/v2/all")
    .then(response => response.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (country)=>{
      this.selectedCountry = country;
    })
  },
  components:{
    "country-list": CountriesList,
    "country-detail": CountryDetail
  }
  }

</script>

<style>
  .main-container{
    display: flex;
    justify-content: space-between;
  }
</style>
