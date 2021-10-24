<template>
  <div v-if="data" class="row content-wrapper">
    <div class="col-lg-12">
      <h3 class="text-center details country-name">Country: {{ data.country }}</h3>
    </div>
    <div class="col-lg-6">
      <h3 class="text-center details confirmed-total">Confirmed: {{ covidData.confirmed }}</h3>
    </div>
    <div class="col-lg-6">
      <h3 class="text-center details deaths-total">Deaths: {{ covidData.deaths }}</h3>
    </div>
    <div class="col-lg-6">
      <h3 class="text-center details fdose-total">First Dose Vaccinate: {{ covidData.fdose_vac }}</h3>
    </div>
    <div class="col-lg-6">
      <h3 class="text-center details sdose-total">Second Dose Vaccinate: {{ covidData.sdose_vac }}</h3>
    </div>
    <div class="col-lg-12">
      <p class="col-xl-12 text-center up-date">Last Updated: {{ data.updated }}</p>
    </div>
  </div>
</template>

<script>
import { onBeforeMount, onUpdated, ref } from 'vue'
import numeral from 'numeral'

export default {
  props: ['covData', 'vacData'],
  setup(props) {
    const data = ref(null)
    const vaccines = ref(null)
    const covidData = ref({
      confirmed: null,
      deaths: null,
      fdose_vac: null,
      sdose_vac: null
    })

    const convertNumber = (value) => {
      return numeral(value).format('0,0')
    }

    onBeforeMount(() => {
      data.value = props.covData
      vaccines.value = props.vacData
      covidData.value.confirmed = convertNumber(data.value.confirmed)
      covidData.value.deaths = convertNumber(data.value.deaths)
      covidData.value.fdose_vac = convertNumber(vaccines.value["people_partially_vaccinated"])
      covidData.value.sdose_vac = convertNumber(vaccines.value["people_vaccinated"])
    })

    onUpdated(() => {
      data.value = props.covData
      vaccines.value = props.vacData
      covidData.value.confirmed = convertNumber(data.value.confirmed)
      covidData.value.deaths = convertNumber(data.value.deaths)
      covidData.value.fdose_vac = convertNumber(vaccines.value["people_partially_vaccinated"])
      covidData.value.sdose_vac = convertNumber(vaccines.value["people_vaccinated"])
    })

    return { data, covidData }
  }
}
</script>

<style>
  @import url('../assets/main.css');
</style>