<template>
  <base-header></base-header>
  <div v-show="selectedCountry">
    <display-data></display-data>
  </div>
</template>

<script>
import { inject, onMounted } from 'vue';
import BaseHeader from '../components/BaseHeader.vue'
import DisplayData from '../components/DisplayData.vue'

export default {
  components: {
    BaseHeader,
    DisplayData
  },
  setup() {
    const selectedCountry = inject('country');

    onMounted(() =>{ 
      console.log(selectedCountry)
    }, DisplayData)

    return {selectedCountry}
  }
}
</script>

<style>

</style>