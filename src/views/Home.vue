<template>
  <div class="container main-container">
    <form @submit.prevent="selectCountry" class="row">
      <div class="col-xl-12 text-center input-wrapper">
        <select class="select" v-model="selected">
          <option selected hidden>Select Country</option>
          <option v-for="country in countryList" :key="country" :value="country">{{ country }}</option>
        </select>
        <input class="input-btn" type="submit" value="Search">
      </div>
    </form>
    <div v-if="vaccines">
      <display-data :covData="covidData" :vacData="vaccines"></display-data>
    </div>
  </div>
</template>

<script>
import { ref} from 'vue';
import axios from 'axios'
import DisplayData from '../components/DisplayData.vue'

export default {
  components: {
    DisplayData
  },
  setup() {
    const selected = ref(null)
    const countryList = ref(null)
    const covidData = ref(null)
    const vaccines = ref(null)

    axios.get('https://covid-api.mmediagroup.fr/v1/cases')
      .then(response => countryList.value = Object.keys(response.data))

    const selectCountry = () => {
      if(!selected.value) {
        return alert('please select a country to continue!')
      }

      axios.get(`https://covid-api.mmediagroup.fr/v1/cases?country=${selected.value}`)
        .then(response => covidData.value = response.data['All'])

      axios.get(`https://covid-api.mmediagroup.fr/v1/vaccines?country=${selected.value}`)
        .then(response => vaccines.value = response.data['All'])
    }

    return {selected, selectCountry, countryList, covidData, vaccines }
  }
}
</script>

<style>
  @import url('../assets/main.css');
</style>