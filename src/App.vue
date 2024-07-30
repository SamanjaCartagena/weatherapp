<template>
  <div class="flex flex-col min-h-screen bg-weather-primary">
    <site-navigation></site-navigation>
    <router-view/>
  </div>
</template>

<script>
import SiteNavigation from './components/SiteNavigation.vue'
export default {
  components: { SiteNavigation },

}
</script>

<style>

</style>