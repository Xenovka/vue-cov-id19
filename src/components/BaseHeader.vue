<template>
  <form @submit.prevent="selectCountry">
    <select name="countries" id="countries" class="select" v-model="selected">
      <option selected disabled>Select Country</option>
      <option v-for="country in countryList" :key="country" :value="country">{{ country }}</option>
    </select>
    <input type="submit" value="Search">
  </form>
</template>

<script>
import { onMounted, provide, ref } from 'vue'
import axios from 'axios'

export default {
  setup() {
    const selected = ref(null)
    const countryList = ref(null)

    onMounted(() =>{ 
      axios.get('https://covid-api.mmediagroup.fr/v1/cases')
        .then(response => countryList.value = Object.keys(response.data))
    })

    const selectCountry = () => {
      if(!selected.value) {
        return alert('select country!')
      }
    }

    provide('country', selected);

    return { selected, selectCountry, countryList }
  }
}
</script>

<style>

</style>