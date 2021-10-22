<template>
  <h1>{{ covidData['All'].country }}</h1>
</template>

<script>
import { onMounted, onUpdated, ref } from 'vue'

export default {
  props: ['country'],
  setup(props) {
    const covidData = ref(null)

    const getData = async (country) => {
      const result = await fetch(`https://covid-api.mmediagroup.fr/v1/cases?country=${country}`)
      covidData.value = await result.json()
    }

    onMounted(async () => {
      await getData(props.country)
      console.log(covidData.value)
    })

    onUpdated(() => {
      getData(props.country)
    })

    return { covidData }
  }
}
</script>

<style>

</style>