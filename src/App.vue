<template>
  <div id="app">
    <TheHeader />
    <Vehicles />
    <TheFooter />
  </div>
</template>
<script>
import TheHeader from '@/modules/header/components/TheHeader.vue'
import Vehicles from '@/modules/vehicles/components/Vehicles.vue'
import TheFooter from '@/modules/footer/components/TheFooter.vue'
export default {
  name: 'App',
  components: {
    TheHeader,
    Vehicles,
    TheFooter
  }
}
</script>