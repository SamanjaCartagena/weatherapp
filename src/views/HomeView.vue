<template>
  <main class="container text-black">
    <div class='pt-4 mb-8 relative'>
      <input 
      v-model="searchQuery"
      @input="getSearchResults"
      type="text" placeholder="Search for a city or a "
      class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-seconndary focus:outline-none
      focus:shadow-[0px_1px_0_0)#004E71]
      "/>
      <ul
      v-if="mapboxSearchResults"
      class='absolute bg-weather-secondary text-black w-full shadow-md py-2 px-1 top-[66px]'>
         <li v-for='searchResult in mapboxSearchResults' :key="searchResult.id"
         class="py-2 cursor-pointer"
         >
           {{searchResult.place_name}}
         </li>

      </ul>
    </div>
  </main>
</template>

<script setup>
import {ref} from 'vue'
import axios from 'axios'

const mapboxSearchResults=ref(null)
const mapoboxAPIKey="pk.eyJ1Ijoic2FtYW5qYTEyMyIsImEiOiJjbHphc2JpeHowcmpzMmlvZDB4MWl1aW9sIn0.8qSiGV_qeMZnorHFoej9JA"
const searchQuery = ref('')
const queryTimeout= ref(null)
const getSearchResults= () => {
  clearTimeout(queryTimeout.value)
  queryTimeout.value=setTimeout(async()=> {
   if (searchQuery.value !== ''){
    const result =await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapoboxAPIKey}&types=place`)
    mapboxSearchResults.value = result.data.features;
    console.log(mapboxSearchResults.value)
    return;
   }
   mapboxSearchResults.value= null
  },300)
}

</script>

<style>

</style>
