<template>
  <div v-if="covidData">
    <h3>Country: {{ covidData.country }}</h3>
    <h3>Confirmed: {{ covidData.confirmed }}</h3>
    <h3>Recovered: {{ covidData.recovered }}</h3>
    <h3>Deaths: {{ covidData.deaths }}</h3>
    <p>Last Updated: {{ covidData.updated }}</p>
  </div>
</template>

<script>
import { onMounted, onUpdated, ref } from 'vue'

export default {
  props: ['covData'],
  setup(props) {
    const covidData = ref(null)

    onMounted(() => {
      covidData.value = props.covData
    })

    onUpdated(() => {
      covidData.value = props.covData
    })

    return { covidData }
  }
}
</script>

<style>

</style>