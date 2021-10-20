<template>
  <form @submit.prevent="searchData">
    <input type="text" name="inputCountry" id="input_country" ref="inputCountry">
  <input type="submit" value="Search">
  </form>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const inputCountry = ref(null)

    const searchData = () => {
      const country = inputCountry.value.value
      inputCountry.value.value = ""
      console.log(country)
    }

    return { inputCountry, searchData }
  }
}
</script>

<style>

</style>