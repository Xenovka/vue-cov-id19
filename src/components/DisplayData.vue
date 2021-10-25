<template>
  <div v-if="data" class="row content-wrapper">
    <div class="col-lg-12">
      <h3 class="text-center country-name">{{ data.country }}</h3>
    </div>
    <div class="col-lg-4 offset-lg-2">
      <div class="text-center details confirmed-total">
        <h3 class="details-title">Confirmed</h3>
        <h3 class="details-text">{{ covidData.confirmed }}</h3>
      </div>
    </div>
    <div class="col-lg-4">
      <div class="text-center details deaths-total">
        <h3 class="details-title">Deaths</h3>
        <h3 class="details-text">{{ covidData.deaths }}</h3>
      </div>
    </div>
    <div class="col-lg-4 offset-lg-2">
      <div class="text-center details fdose-total">
        <h3 class="details-title">First Vaccination</h3>
        <h3 class="details-text">{{ covidData.fdose_vac }}</h3>
      </div>
    </div>
    <div class="col-lg-4">
      <div class="text-center details sdose-total">
        <h3 class="details-title">Second Vaccination</h3>
        <h3 class="details-text">{{ covidData.sdose_vac }}</h3>
      </div>
    </div>
    <div class="col-lg-12">
      <p class="text-center up-date">Data Updated {{ updateTime }}</p>
    </div>
    <div class="col-lg-12">
      <p class="text-center footer-text">Made with ♥ using Vue.js and the data from 
        <a class="footer-link" href="https://github.com/M-Media-Group/Covid-19-API">MMedia Group</a>.
      </p>
    </div>
  </div>
</template>

<script>
import { onBeforeMount, onUpdated, ref } from 'vue'
import numeral from 'numeral'
import Moment from 'moment'

export default {
  props: ['covData', 'vacData'],
  setup(props) {
    const data = ref(null)
    const vaccines = ref(null)
    const getTime = ref(null)
    const updateTime = ref(null)
    const covidData = ref({
      confirmed: null,
      deaths: null,
      fdose_vac: null,
      sdose_vac: null
    })

    const convertNumber = (value) => {
      return numeral(value).format('0,0')
    }

    getTime.value = new Date(props.covData.updated).toISOString()
    updateTime.value = Moment(getTime).fromNow()

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

    return { data, covidData, updateTime }
  }
}
</script>

<style>
  @import url('../assets/main.css');
</style>