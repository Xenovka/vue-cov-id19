<template>
  <form @submit.prevent="selectCountry">
    <select name="countries" id="countries" class="select" v-model="selected">
      <option value="select" selected disabled>Select Country</option>
      <option v-for="country in countryList" :key="country" :value="country">{{ country }}</option>
    </select>
    <input type="submit" value="Search">
  </form>
  <div v-if="isSelected">
    <display-data :country="selected"></display-data>
  </div>
</template>

<script>
import { onMounted, ref} from 'vue';
import axios from 'axios'
import DisplayData from '../components/DisplayData.vue'

export default {
  components: {
    DisplayData
  },
  setup() {
    const selected = ref(null)
    const countryList = ref(null)
    const isSelected = ref(false)

    onMounted(() =>{ 
      axios.get('https://covid-api.mmediagroup.fr/v1/cases')
        .then(response => countryList.value = Object.keys(response.data))
    })

    const selectCountry = () => {
      if(!selected.value) {
        return alert('please select a country to continue!')
      }

      isSelected.value = true
    }

    return {selected, selectCountry, countryList, isSelected }
  }
}
</script>

<style>

</style>